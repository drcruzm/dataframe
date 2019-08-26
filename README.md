# Aprendiendo a analizar DataFrames
----------

title: "clima"
author: "Dr Victor"
date: "19 de junio de 2019"
output: html_document

## runtime: shiny
    knitr::opts_chunk$set(echo = TRUE)
    # setwd("C:/Users/Dr.Victor/Dropbox/R code")
    getwd()
    clima <- read.table("https://drvcruz.s3.us-east-2.amazonaws.com/SilwoodWeather.txt",header = T)
    #library(ggplot2)
    names(clima)
    attach(clima)
    head(clima)
    str(clima)
    month<-factor(month)
    
## Gráficas tipo box Plot
    plot(month,upper)
    library(ggplot2)
    month<-factor(month)
    is.factor(month)
    plot(month,upper)
    p1 <- ggplot(clima, aes(x = factor(month), y = upper))+geom_boxplot()
    p1
    
## Instalando Plotly
    #install.packages("plotly")
    library(plotly)
    
## Calculo de los cuantiles
    quantile(clima$upper) # para todos los años
    
## Repetimos para lower
    pp <- ggplot(clima, aes(x = factor(month), y = lower)) + geom_boxplot()
    pp
    ggplotly(pp)
     quantile(clima$lower)  #Para todos los AÑOS
     
## Análisis para todos los años del mes 3 en lower
    sub1<-subset(clima, month=="3")
    
## AHORA EL FACTOR ES AÑO
    mes3 <- ggplot(clima, aes(x = factor(yr), y = lower)) + geom_boxplot()
    
    ggplotly(mes3)
    
    boxplot(factor(sub1$yr), sub1$lower)
    
    median(sub1$lower)
    
    quantile(sub1$lower)#SOLO PARA EL MES 3
    sd(sub1$lower)
    (6-0.5)*0.75
    
## Graficando sus Frecuencias mes 3
    hist(sub1$lower,freq = T, col = "lightblue",main = "lower levels month 3")
    abline(v=mean(sub1$lower), col=3)
    abline(v=4.125, col=2)
    quantile(sub1$lower)
    
## Ahora solo para el mes 3 año 1996
    sub2 <- subset(sub1, yr==1996)
    
    dias3 <- ggplot(sub2, aes(x=1:31,y=lower),xlab("dias")) + geom_point()
    
    ggplotly(dias3)
    
    quantile(sub2$lower)
    median(sub2$lower)
    
    summary(sub2$lower)
    
## Grafica del Mes 3 de 1996
    par(mfrow=c(1,2))
    
    hist(sub2$lower,freq = T, col = "lightblue",main = "lower levels month 3")
    abline(v=median(sub2$lower), col="red")
    abline(v= -1.9, col=4)
    abline(v=2.25, col="green")
    
    boxplot(sub2$lower)
    grid()


