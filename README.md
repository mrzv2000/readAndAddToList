#ifndef MAINWINDOW_H
#define MAINWINDOW_H

#include <QMainWindow>
#include "read.h"


QT_BEGIN_NAMESPACE
namespace Ui { class MainWindow; }
QT_END_NAMESPACE

class MainWindow : public QMainWindow
{
    Q_OBJECT

public:
    MainWindow(QWidget *parent = nullptr);
    ~MainWindow();

private slots:



    void on_showB_clicked();

private:
    read obj1;
    Ui::MainWindow *ui;
};
#endif // MAINWINDOW_H
---------------------------------------------------------------------------
  #ifndef READ_H
#define READ_H
#include<QString>
#include<QVector>
using namespace std;



class read
{
public:
    QVector<QString> info;
    void save(QString);
    void readFromFile(QString);
    read();


};

#endif // READ_H
----------------------------------------------------------------------------
  #include "mainwindow.h"
#include "ui_mainwindow.h"
#include <QStringListModel>

MainWindow::MainWindow(QWidget *parent)
    : QMainWindow(parent)
    , ui(new Ui::MainWindow)
{
    ui->setupUi(this);

}

MainWindow::~MainWindow()
{
    delete ui;
}



//void MainWindow::on_showB_clicked()
//{
////    QStringListModel *model = new QStringListModel(this);
////    obj1.readFromFile("testingText.txt");
////    for(int i=0 ; i<obj1.info.size() ; i++){
////        model->insertRow(model->rowCount());
////        QModelIndex index = model->index(model->rowCount()-1);
////        model->setData(index, obj1.info[i]);

////    }
//}


void MainWindow::on_showB_clicked()
{
    //qDebug()<<"salam";
    QStringListModel *model = new QStringListModel(this);
    ui->listVect->setModel(model);
    qDebug()<<"salam";
    obj1.readFromFile("testingText");
    for(int i=0 ; i<obj1.info.size() ; i++){
        qDebug()<<"salam";
        model->insertRow(model->rowCount());
        QModelIndex index = model->index(model->rowCount()-1);
        model->setData(index, obj1.info[i]);

        qDebug()<<obj1.info[i];
    }
}
-------------------------------------------------------------------------------------------
  #include "read.h"
#include<QFile>
#include<QTextStream>
#include<QMessageBox>
read::read()
{

}
void read::save(QString information){
    info.push_back(information);
}
void read::readFromFile(QString fileName){
    QFile file(fileName);
    if(!file.open(QIODevice::ReadOnly)){
        QString warning = "File Not Found";
    }else{
        QTextStream stream (&file);
        while (!stream.atEnd()){
            save(stream.readLine());
        }
    }
}
