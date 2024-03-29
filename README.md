# Análisis de Factores

Analisis de Datos con Plottly y Factor


## Seleccion del directorio
```{r}
knitr::opts_chunk$set(echo = TRUE)
setwd("C:/Users/Dr.Victor/Dropbox/R code")
getwd()
```

## Lectura de Datos
```{r}
clima <- read.table("https://drvcruz.s3.us-east-2.amazonaws.com/SilwoodWeather.txt",header = T)
```

## library(ggplot2)

```{r}
library(ggplot2)
names(clima)
attach(clima)
head(clima)
str(clima)
month<-factor(month)
```

## Gráficas tipo box Plot
```{r}
plot(month,upper)
```

## Gráficas tipo FACTOR
```{r}
month<-factor(month)
is.factor(month)
plot(month,upper)
```

## Gráfica Completa mes vs upper limit

```{r}
p1 <- ggplot(clima, aes(x = factor(month), y = upper))+geom_boxplot()
p1
```

## Instalando Plotly

```{r}
#install.packages("plotly")
library(plotly)
```


## Calculo de los cuantiles

```{r}
quantile(clima$upper) # para el año
```

## Repetimos para lower limit

```{r}
pp <- ggplot(clima, aes(x = factor(month), y = lower)) + geom_boxplot()
pp
  ggplotly(pp)
 quantile(clima$lower)  #Para todos los AÑOS
```

## Analisis para todos los años del mes 3 en lower

```{r}
sub1<-subset(clima, month=="3")

## AHORA EL FACTOR ES AÑO

mes3 <- ggplot(sub1, aes(x = factor(yr), y = lower)) + geom_boxplot()

ggplotly(mes3)

median(sub1$lower)

boxplot(sub1$lower) # Cuantil del mes 3 para todos los años 1987-2005
grid(10)

quantile(sub1$lower)#SOLO PARA EL MES 3
sd(sub1$lower)
(6-0.5)*0.75
```

## Graficando sus Frecuencias mes 3

```{r}
hist(sub1$lower,freq = T, col = "lightblue",main = "lower levels month 3")
abline(v=mean(sub1$lower), col=3)
abline(v=6, col=2)
quantile(sub1$lower)
```

## Ahora solo para el mes 3 año 1996

```{r}
sub2 <- subset(sub1, yr==1996)

head(sub2)
diasmes3 <- ggplot(sub2, aes(x=1:31,y=lower),xlab("dias")) + geom_point()

ggplotly(diasmes3)

quantile(sub2$lower)
median(sub2$lower)

summary(sub2$lower)
```

## Grafica del Mes 3 de 1996

```{r}
par(mfrow=c(1,2))

hist(sub2$lower,freq = T, col = "lightblue",main = "lower levels month 3")
# Grafica cuantiles sobre histograma
abline(v=median(sub2$lower), col="red")
abline(v= -1.9, col=4)
abline(v=2.25, col="green")

boxplot(sub2$lower)
grid()
```

## Quantile rain

```{r}
quantile(clima$rain)
```
## Rain
```{r}
p1 <- ggplot(clima, aes(x = factor(month), y = rain)) + geom_boxplot()
ggplotly(p1)
```

## Rain upper Limit
```{r}
yr <-factor(yr)
p3 <- ggplot(clima, aes(x = factor(yr), y = upper)) + geom_boxplot()

ggplotly(p3)
```
