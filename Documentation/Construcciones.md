# Construcciones



## Introducci�n


El proyecto de Construcciones consta en poder filmar un plano de construcci�n ya predeterminado y, con realidad aumentada (RA) poder mostrar virtualmente las paredes y las columnas de dicha construcci�n, pudiendo visualizar gr�ficamente la intensidad de las cargas aplicadas a lo largo de las v�as.



## Usabilidad


_[En esta secci�n se pretende mostrar la aplicaci�n a trav�s de texto, videos e im�genes, explicando los botones y dem�s. Completar cuando se tenga algo contundente]_



## Estructura del proyecto


Dentro de la jerarqu�a de la escena de _Construcciones_ se pueden observar cinco objetos. Ellos son: Directional Light, ARCamera, ImageTarget, Canvas y EventSystem.  


**Directional Light** contiene una luz direccional para iluminar la escena. Los detalles de la misma no tienen mayor relevancia. **EventSystem** es un objeto propio de Unity dedicado a manejar la escena. Los detalles del mismo se especifican mejor en la [documentaci�n de Unity](https://docs.unity3d.com/ScriptReference/EventSystems.EventSystem.html). **ARCamera** es el objecto que contiene el componente de la c�mara de la escena (notar que la c�mara de la escena no es la c�mara fotogr�fica del dispositivo). Esta c�mara tiene a su vez el script _Vuforia Behaviour_ que se encarga de mostrar la c�mara del dispositivo y detectar autom�ticamente las im�genes (Image Targets). Vale aclarar que todo esto lo maneja Vuforia, y que de parte del desarrollador no resta m�s que crearlo y hacer las configuraciones m�nimas.  


Los objetos restantes, **ImageTarget** y **Canvas** se describen en las subsecciones siguientes



### ImageTarget

Los objectos ImageTarget de Vuforia son los que contienen la imagen a escanear y tambi�n los objetos virtuales a mostrar. Los componentes que estos objetos incluyen ya vienen predeterminadamente configurados por Vuforia. S�lo hay que configurar el componente 'Image Target Behaviour', especificando la base de datos de Vuforia y la textura a capturar.

Todos los objetos virtuales que se renderizar�n al encontrar el plano deben ser hijos de ImageTarget, y con eso es suficiente. Los scripts de Vuforia (especificamente DefaultTrackableEventHandler.cs) se encargar�n de mostrarlos cuando se detecte el plano. Espec�ficamente para este proyecto, tenemos dos grupos principales de objetos virtuales: **Cargas** y **Edificio**. El objeto Edificio contiene las paredes, columnas y el techo que se renderiza. Dado que las paredes se tornan 50% transparentes al mostrar las cargas es necesario que el material que las compone	tenga setteado el modo de rendering en _Transparente_.  

El objeto Cargas contiene las gr�ficas de las cargas que cada viga soporta a lo largo de la misma. Estas gr�ficas no son m�s que sprites en .png colocadas en la escena de una manera predeterminada.



### Canvas

El objeto Canvas contiene la UI de la aplicaci�n. Esto incluye el bot�n FocusButton, la barra lateral SideBar y el objeto CambioDeEscenas. El objeto **FocusButton** maneja el foco de la c�mara del dispositivo para poder enfocar mejor el plano f�sico. Se implement� especialmente para casos donde la c�mara del dispositivo no sea muy buena.  

La barra lateral **Side Bar** incluye tres botones: BotonAumentos, BotonVolver y BotonCargas. El primero permite navegar entre proyectos (como ser SistemaPlanetario, Peralte o Construcciones mismo). La l�gica del cambio de escenas se encuentra en el objeto CambioDeEscenas. El bot�n **BotonCargas** permite mostrar u ocultar las cargas de las vigas en la escena. El script que maneja su l�gica es ShowLoads.cs y se encuentra en `Assets/Custom/Scripts/ShowLoads.cs`