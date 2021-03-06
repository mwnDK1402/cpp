
 

 

 

 

 

([C++](Cpp.md)) [QtBrownianMotion](CppQtBrownianMotion.md)
============================================================

 

Technical facts
---------------

 

 

 

 

 

 

./CppQtBrownianMotion/CppQtBrownianMotion.pri
---------------------------------------------

 

  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` INCLUDEPATH += \     ../../Classes/CppQtBrownianMotion  HEADERS += \     ../../Classes/CppQtBrownianMotion/qtbrownianmotionparameterswidget.h \     ../../Classes/CppQtBrownianMotion/qtbrownianmotionmaxlikelihoodwidget.h \     ../../Classes/CppQtBrownianMotion/qtbrownianmotionlikelihoodwidget.h  SOURCES += \     ../../Classes/CppQtBrownianMotion/qtbrownianmotionparameterswidget.cpp \     ../../Classes/CppQtBrownianMotion/qtbrownianmotionmaxlikelihoodwidget.cpp \     ../../Classes/CppQtBrownianMotion/qtbrownianmotionlikelihoodwidget.cpp  FORMS += \     ../../Classes/CppQtBrownianMotion/qtbrownianmotionparameterswidget.ui \     ../../Classes/CppQtBrownianMotion/qtbrownianmotionmaxlikelihoodwidget.ui \     ../../Classes/CppQtBrownianMotion/qtbrownianmotionlikelihoodwidget.ui  OTHER_FILES += \     ../../Classes/CppQtBrownianMotion/Licence.txt`
  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppQtBrownianMotion/qtbrownianmotionlikelihoodwidget.h
--------------------------------------------------------

 

  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #ifndef QTBROWNIANMOTIONLIKELIHOODWIDGET_H #define QTBROWNIANMOTIONLIKELIHOODWIDGET_H  #include <QWidget>  namespace Ui { class QtBrownianMotionLikelihoodWidget; }  class QtBrownianMotionLikelihoodWidget : public QWidget {   Q_OBJECT  public:   explicit QtBrownianMotionLikelihoodWidget(QWidget *parent = 0);   ~QtBrownianMotionLikelihoodWidget();    void CalcLikelihood(const std::vector<double>& v) noexcept;  signals:   void signal_parameters_changed();  private:   Ui::QtBrownianMotionLikelihoodWidget *ui;  private slots:   void OnAnyChange() noexcept; };  #endif // QTBROWNIANMOTIONLIKELIHOODWIDGET_H`
  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppQtBrownianMotion/qtbrownianmotionlikelihoodwidget.cpp
----------------------------------------------------------

 

  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include "qtbrownianmotionlikelihoodwidget.h"  #include "brownianmotionhelper.h"  #include "ui_qtbrownianmotionlikelihoodwidget.h"  QtBrownianMotionLikelihoodWidget::QtBrownianMotionLikelihoodWidget(QWidget *parent) :   QWidget(parent),   ui(new Ui::QtBrownianMotionLikelihoodWidget) {   ui->setupUi(this);   QObject::connect(ui->box_cand_volatility,SIGNAL(valueChanged(double)),this,SLOT(OnAnyChange())); }  QtBrownianMotionLikelihoodWidget::~QtBrownianMotionLikelihoodWidget() {   delete ui; }  void QtBrownianMotionLikelihoodWidget::CalcLikelihood(   const std::vector<double>& v ) noexcept {   const auto cand_volatility     = ui->box_cand_volatility->value() / boost::units::si::second;    if (v.size() <= 2) return;    const double log_likelihood{     ribi::bm::Helper().CalcLogLikelihood(       v,       cand_volatility * cand_volatility     )   };   ui->edit_log_likelihood->setText(std::to_string(log_likelihood).c_str()); }  void QtBrownianMotionLikelihoodWidget::OnAnyChange() noexcept {   emit signal_parameters_changed(); }`
  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppQtBrownianMotion/qtbrownianmotionmaxlikelihoodwidget.h
-----------------------------------------------------------

 

  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #ifndef QTBROWNIANMOTIONMAXLIKELIHOODWIDGET_H #define QTBROWNIANMOTIONMAXLIKELIHOODWIDGET_H  #include <QWidget>  namespace Ui { class QtBrownianMotionMaxLikelihoodWidget; }  class QtBrownianMotionMaxLikelihoodWidget : public QWidget {   Q_OBJECT  public:   explicit QtBrownianMotionMaxLikelihoodWidget(QWidget *parent = 0);   ~QtBrownianMotionMaxLikelihoodWidget();    double GetMaxLogLikelihood() const noexcept { return m_max_log_likelihood; }   void SetData(const std::vector<double>& v);  private:   Ui::QtBrownianMotionMaxLikelihoodWidget *ui;   double m_max_log_likelihood; };  #endif // QTBROWNIANMOTIONMAXLIKELIHOODWIDGET_H`
  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppQtBrownianMotion/qtbrownianmotionmaxlikelihoodwidget.cpp
-------------------------------------------------------------

 

  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include "qtbrownianmotionmaxlikelihoodwidget.h"  #include "brownianmotionhelper.h"  #include "ui_qtbrownianmotionmaxlikelihoodwidget.h"  QtBrownianMotionMaxLikelihoodWidget::QtBrownianMotionMaxLikelihoodWidget(QWidget *parent) :   QWidget(parent),   ui(new Ui::QtBrownianMotionMaxLikelihoodWidget) {   ui->setupUi(this); }  QtBrownianMotionMaxLikelihoodWidget::~QtBrownianMotionMaxLikelihoodWidget() {   delete ui; }  void QtBrownianMotionMaxLikelihoodWidget::SetData(const std::vector<double>& v) {   auto volatility_hat = 0.0 / boost::units::si::second;   ribi::bm::Helper().CalcMaxLikelihood(v,volatility_hat);   ui->edit_sigma_hat->setText(std::to_string(volatility_hat.value()).c_str());   m_max_log_likelihood     = ribi::bm::Helper().CalcLogLikelihood(v,volatility_hat * volatility_hat)   ;   ui->edit_max_log_likelihood->setText(std::to_string(m_max_log_likelihood).c_str()); }`
  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppQtBrownianMotion/qtbrownianmotionparameterswidget.h
--------------------------------------------------------

 

  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #ifndef QTBROWNIANMOTIONPARAMETERSWIDGET_H #define QTBROWNIANMOTIONPARAMETERSWIDGET_H  #include <QWidget>  namespace Ui { class QtBrownianMotionParametersWidget; }  class QtBrownianMotionParametersWidget : public QWidget {   Q_OBJECT  public:   explicit QtBrownianMotionParametersWidget(QWidget *parent = 0);   ~QtBrownianMotionParametersWidget();      double GetInitValue() const noexcept;   int GetEndTime() const noexcept;    ///noise: sigma   double GetVolatility() const noexcept;    int GetSeed() const noexcept;  signals:   void signal_parameters_changed();  private:   Ui::QtBrownianMotionParametersWidget *ui;  private slots:   void OnAnyChange() noexcept; };  #endif // QTBROWNIANMOTIONPARAMETERSWIDGET_H`
  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

./CppQtBrownianMotion/qtbrownianmotionparameterswidget.cpp
----------------------------------------------------------

 

  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  ` #include "qtbrownianmotionparameterswidget.h"  #include "brownianmotion.h"  #include "ui_qtbrownianmotionparameterswidget.h"  QtBrownianMotionParametersWidget::QtBrownianMotionParametersWidget(QWidget *parent) :   QWidget(parent),   ui(new Ui::QtBrownianMotionParametersWidget) {   ui->setupUi(this);    QObject::connect(ui->box_init_x,SIGNAL(valueChanged(double)),this,SLOT(OnAnyChange()));   QObject::connect(ui->box_t_end,SIGNAL(valueChanged(int)),this,SLOT(OnAnyChange()));   QObject::connect(ui->box_volatility,SIGNAL(valueChanged(double)),this,SLOT(OnAnyChange()));   QObject::connect(ui->box_seed,SIGNAL(valueChanged(int)),this,SLOT(OnAnyChange())); }  QtBrownianMotionParametersWidget::~QtBrownianMotionParametersWidget() {   delete ui; }  double QtBrownianMotionParametersWidget::GetInitValue() const noexcept {   return ui->box_init_x->value(); }  int QtBrownianMotionParametersWidget::GetEndTime() const noexcept {   return ui->box_t_end->value(); }  double QtBrownianMotionParametersWidget::GetVolatility() const noexcept {   return ui->box_volatility->value(); }  int QtBrownianMotionParametersWidget::GetSeed() const noexcept {   return ui->box_seed->value(); }  void QtBrownianMotionParametersWidget::OnAnyChange() noexcept {   emit signal_parameters_changed(); }`
  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 

 

 

 

 

 

