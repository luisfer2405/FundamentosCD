# FundamentosCD

# Fundamentos de datos
## actividades practicas

en el siguiente readme dejamos la informacion del projecto 

Linda Marcela Villamil Ortigoza 

DBanner: 100173668

Luis Fernando Montero Castro 

IDBanner: 100164000

Corporación Universitaria Iberoamericana 

Ingeniería de Ciencia de Datos






# Actividad 3 parte1

Ciencia de datos en acción - Fase 1 (Practicando con R)
El objetivo de esta actividad es realizar algunas actividades prácticas que permitan
identificar patrones y realizar análisis en conjuntos de datos con RStudio. Se espera que los
estudiantes al desarrollar estos ejercicios, se motive a expandir las posibilidades que ofrece
la herramienta y amplíe los conceptos trabajados en el curso


## Ejercicio 1
Cada grupo de estudiantes debe crear un conjunto de datos de 30 estudiantes de un curso
de Fundamentos de ciencia de datos, los datos que se deben relacionar por cada estudiante
son:
● Sexo
● Edad,
● Estatura
● Nota
● Ciudad
Con estos datos y usando la herramienta RStudio cada grupo debe:




### 1 Realizar una tabla de frecuencias absolutas y otra de frecuencias relativas para la
### variable Calificación. Almacena las tablas anteriores en dos variables y llámalas
### absolutas y relativas.



## frecuencias absolutas
```R
#Calcular la tabla de frecuencias absolutas para la variable Calificación
absolutas <- table(df$Nota)
print(absolutas) 
```
![Punto 1.1](img/1-1.png)

## frecuencias relativas
```R
calcular la tabla de frecuencias relativas para la variable nota.
relativas <- prop.table(table(df$Nota))
relativas
```
![Punto 1.2](img/1-2.png)




### 2. Representar la variable ciudad mediante un diagrama de barras y un diagrama de
### sectores. Incluye un título adecuado para cada gráfico y colorea las barras y los
### sectores de colores diferentes.




## Diagrama de barras
```R
    barras <- ggplot(df, aes(x = Ciudad, fill = Ciudad)) +
    geom_bar() +
     labs(title = "Diagrama de Barras - Ciudad") +
    theme_minimal()

barras   
```
![Punto 2.1](img/2-1.png)

## Diagrama por sectores
```R
sectores <- ggplot(df , aes(x = "", fill = Ciudad)) +
    geom_bar(width = 1) +
    coord_polar(theta = "y") +
    labs(title = "Diagrama de Sectores - Ciudad") +
    theme_void()

sectores
```
![Punto 2.2](img/2-2.png)


### 3.Para la variable Edad, realizar un histograma y un diagrama de caja y bigotes
### considerando la opción range = 1.5. Incluye un título apropiado para cada gráfico y
### colorea las barras del histograma de color amarillo. ¿Existe algún valor atípico en
### esta variable? Reduce el valor del argumento range hasta 0.5. ¿Varían las
### conclusiones?


```R
histograma_1_5 <- ggplot(df, aes(x = Edad, fill = "Edad")) +
    geom_histogram(binwidth = 1, color = "black", fill = "yellow") +
    labs(title = "Histograma de Edad (Range = 1.5)", x = "Edad", y = "Frecuencia") +
    theme_minimal()

histograma_1_5
```
![Punto 3.1](img/3-1.png)


## caja de bigote range = 1.5
```R
#se ccrea la caja de bigote con rango 1.5
caja_bigotes_1_5 <- ggplot(df, aes(x = "", y = Edad, fill = "Edad")) +
    geom_boxplot() +
    labs(title = "Diagrama de Caja y Bigotes de Edad (Range = 1.5)", y = "Edad") +
    theme_minimal()

```
![Punto 3.2](img/3-2.png)


## caja y bigotes con range = 0.5+
```R
boxplot_5_ <- ggplot(df, aes(y=Edad)) +
  geom_boxplot()+
  labs(title = "Diagrama de caja y bigotes - range = 0.5", x="") +
  coord_cartesian(ylim = quantile(df$Edad, c(0.25, 0.75)) + 0.5 * IQR(df$Edad)) 
print(boxplot_5_)

print(boxplot_5_)
```
![Punto 3.2.1](img/3.2.1.png)


Se puede obervar que en la caja de bigotes de range 0.5 no se visualiza algunos datos lo cual no da imagen total de los datos.




### 4. Realizar un resumen de la variable Puntuación mediante la orden summary.
### Comprueba que las medidas que proporciona summary coinciden con las medidas
### calculadas de forma individual usando su función específica.

```R
summary(df)
``` 
![Punto 4.1](img/4-1.png)
```R
mean(df$Nota)
median(df$Nota)
min(df$Nota)
max(df$Nota)
quantile(df$Nota, probs = c(0.25, 0.5, 0.75))

``` 
![Punto 4.2](img/4.1.1.png)

### 5. Calcular la estatura media de los estudiantes y proporcionar al menos, dos
### medidas que indiquen la dispersión de esta variable.

```R
mean(df$Estatura)
sd(df$Estatura)
IQR(df$Estatura)

```
![Punto 5.1](img/5.1.png)


### 6. Finalmente se espera que el grupo presente las conclusiones a las que puede llegar
### con el desarrollo del taller.


## se llego a lassiguientes conclusiones de que en este conjunto de datos:

- la nota mas repetida en elcurso es la de 35 con 16 % de aparicion.

- la media de estatura eb el grupo es de 168.1.

- los estudiates viven en Barranquilla luego Madrid y bogota
siendo Barranquilla el que mas estudiantes poseen.

-  la edad mas recurrente en los estudiantes es de 18.

- la persona con mas edad del curso tiene 50 años.

- la persona mas alta del curso mide 1.87. 

- la persona mas pequeña del curso mide 1.50.

# Actividad 3 parte2


## Ejercicio 2

Cada grupo de estudiantes trabajará con dos grupos de datos (Gr1, Gr2) de 20 personas para un análisis de, los datos se comparten a continuación


### 1Representar la variable Grupo Sanguíneo mediante un diagrama de sectores en cada uno de los grupos. Incluir un título descriptivo en cada gráfico y colorear los sectores de azul, amarillo, rosa y verde.



```R
grupo_counts1 <- table(g1$Grupo.Sanguineo)


# Colores para cada grupo sanguíneo
colores <- c("#3366CC", "#FFD700", "#FF69B4", "#228B22")  # Azul, Amarillo, Rosa, Verde

df1 <- data.frame(grupo = names(grupo_counts1), count = as.numeric(grupo_counts1))

# Crear el gráfico de sectores con ggplot2

ggplot(df1, aes(x = "", y = count, fill = grupo)) +
    geom_bar(width = 1, stat = "identity", color = "black", size = 1.5, position = "fill") +
    coord_polar(theta = "y") +
        scale_fill_manual(values = colores) +
    labs(title = "Distribución de Grupo Sanguíneo") +
    theme_void() +
    theme(legend.position = "bottom",
        panel.border = element_rect(color = "black", fill = NA, size = 2),
        plot.title = element_text(hjust = 0.5, size = 16, face = "bold", margin = margin(b = 20)),
        plot.margin = margin(10, 10, 10, 10, unit = "pt"),
        plot.background = element_rect(fill = "white", color = "black", size = 1.5),
        panel.grid.minor = element_blank(),
        plot.caption = element_text(hjust = 0.5, size = 12, margin = margin(t = 10)))
grupo_counts <- table(g1$Grupo.Sanguineo)
```




grupo_counts2 <- table(g2$Grupo.Sanguineo)


df2 <- data.frame(grupo = names(grupo_counts2), count = as.numeric(grupo_counts2))

# Crear el gráfico de sectores con ggplot2
ggplot(df2, aes(x = "", y = count, fill = grupo)) +
  geom_bar(width = 1, stat = "identity", color = "black", size = 1.5, position = "fill") +
  coord_polar(theta = "y") +
  scale_fill_manual(values = colores) +
  labs(title = "Distribución de Grupo Sanguíneo") +
  theme_void() +
  theme(legend.position = "bottom",
        panel.border = element_rect(color = "black", fill = NA, size = 2),
        plot.title = element_text(hjust = 0.5, size = 16, face = "bold", margin = margin(b = 20)),
        plot.margin = margin(10, 10, 10, 10, unit = "pt"),
        plot.background = element_rect(fill = "white", color = "black", size = 1.5),
        panel.grid.minor = element_blank(),
        plot.caption = element_text(hjust = 0.5, size = 12, margin = margin(t = 10)))
