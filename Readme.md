# Moogle!

![](moogle.png)

> Proyecto de Programación I.
> Facultad de Matemática y Computación - Universidad de La Habana.
> Cursos 2021, 2022.

Moogle! es una aplicación *totalmente original* cuyo propósito es buscar inteligentemente un texto en un conjunto de documentos.





## Sobre el contenido a buscar

La idea original del proyecto es buscar en un conjunto de archivos de texto (con extensión `.txt`) que estén en la carpeta `Content`. 
## Ejecutando el proyecto

Lo primero que tendrás que hacer para poder trabajar en este proyecto es instalar .NET Core 6.0 (lo que a esta altura imaginamos que no sea un problema, ¿verdad?). Luego, solo te debes parar en la carpeta del proyecto y ejecutar en la terminal de Linux:

```bash
make dev
```

Si estás en Windows, debes poder hacer lo mismo desde la terminal del WSL (Windows Subsystem for Linux). Si no tienes WSL ni posibilidad de instalarlo, deberías considerar seriamente instalar Linux, pero si de todas formas te empeñas en desarrollar el proyecto en Windows, el comando *ultimate* para ejecutar la aplicación es (desde la carpeta raíz del proyecto):
(este es el q yo utilizo para ejecutarlo en la terminal)
```bash
dotnet watch run --project MoogleServer
```

#A continuación, se explica el propósito y funcionamiento de los métodos presentes en el código:

LeerArchivosDeTexto(): Este método lee los archivos de texto que se encuentran en la carpeta "content" y devuelve dos arreglos: uno con el contenido de cada archivo y otro con los nombres de los archivos.

CalcularMatrizTfIdf(string[] documentos, string[] nombresDocumentos): Este método recibe una lista de documentos y sus nombres y devuelve una matriz de TF-IDF. La matriz tiene una fila por cada documento y una columna por cada término (palabra) que aparece en los documentos. Cada celda de la matriz contiene el valor TF-IDF correspondiente a la frecuencia del término en el documento y su frecuencia en todo el conjunto de documentos.

ObtenerPalabras(string texto): Este método recibe un texto y devuelve una lista de las palabras que aparecen en él.

ObtenerPalabrasQuery(string query): Este método recibe una consulta (query) y devuelve una lista de las palabras que aparecen en ella.

CalcularVectorTfIdfQuery(string[] terminos, Dictionary<string, List<string>> frecuencia, string[] palabrasQuery): Este método recibe una lista de términos, la frecuencia de cada término en cada documento y una consulta, y devuelve un vector de TF-IDF para la consulta. El vector tiene una posición para cada término y contiene el valor TF-IDF del término en la consulta.

CalcularSimilitudCoseno(double[] vector1, double[] vector2): Este método recibe dos vectores y devuelve la similitud de coseno entre ellos. La similitud de coseno es una medida de la similitud entre dos vectores que varía entre -1 y 1, donde 1 indica que los vectores son idénticos y -1 indica que son opuestos.

CalcularSimilitudQuery(string query, string[] nombres, string[] contenido, double[,] matriz, Dictionary<string, List<string>> frecuencia): Este método recibe una consulta, los nombres y el contenido de los documentos, una matriz de TF-IDF y la frecuencia de cada término en cada documento, y devuelve un arreglo de similitudes de coseno entre la consulta y los documentos.

ElAprobado(): Este método es un constructor que se encarga de leer los documentos de la carpeta "content" y calcular la matriz de TF-IDF.

Busqueda(string query): Este método recibe una consulta, calcula la similitud de coseno entre la consulta y los documentos, los ordena por similitud descendente y devuelve un arreglo de objetos SearchItem que contiene información sobre los documentos más similares a la consulta. Cada objeto SearchItem contiene el nombre del documento, las primeras 10 palabras del contenido y la similitud de coseno correspondiente.