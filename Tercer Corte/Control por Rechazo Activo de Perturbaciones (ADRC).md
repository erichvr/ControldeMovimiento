
# Control por Rechazo Activo de Perturbaciones (ADRC): Fundamentos, Implementaciones y Aplicaciones Industriales

El Control por Rechazo Activo de Perturbaciones (ADRC) representa un paradigma moderno en ingeniería de control que ha experimentado un desarrollo significativo tanto en sus fundamentos teóricos como en sus implementaciones prácticas. Esta metodología, originalmente propuesta por Jingqing Han en los años 1990, se ha consolidado como una solución robusta para sistemas con dinámicas complejas y desconocidas, ofreciendo ventajas sustanciales frente a métodos tradicionales en escenarios con perturbaciones variables y modelado impreciso[^1][^6].

## Fundamentos Teóricos del ADRC

### Filosofía del Rechazo Activo de Perturbaciones

El ADRC se fundamenta en el concepto de "perturbación total", que unifica todas las incertidumbres del sistema (no linealidades, perturbaciones externas, errores de modelado) en una única variable que puede ser estimada y compensada en tiempo real[^1][^6]. Esta filosofía permite transformar sistemas no lineales complejos en sistemas lineales simplificados mediante el uso de un Observador de Estado Extendido (ESO).

La metodología ADRC trata al modelo desconocido del sistema como un estado especial, denominado "estado extendido", y diseña un observador especial (ESO) para estimar el sistema en tiempo real[^6]. Esta aproximación elimina la necesidad de un modelo matemático detallado de la planta, lo que constituye un avance significativo en la ciencia del control.

### Arquitectura y Componentes Fundamentales

El ADRC está compuesto por tres elementos principales que trabajan de manera sinérgica[^1][^6]:

1. **Mecanismo de seguimiento de trayectoria (TD)**: Genera señales de referencia suaves y diferenciables
2. **Observador de Estado Extendido (ESO)**: Estima tanto los estados del sistema como la perturbación total
3. **Ley de control no lineal (NLSEF)**: Compensa activamente las perturbaciones estimadas

El ESO para un sistema de segundo orden se define mediante el siguiente sistema de ecuaciones:

$$
\begin{cases} 
\dot{z}_1 = z_2 + \beta_1 e \\ 
\dot{z}_2 = z_3 + b_0 u + \beta_2 e \\ 
\dot{z}_3 = \beta_3 e
\end{cases}
$$

donde $e = y - z_1$ representa el error de estimación y $\beta_i$ son ganancias ajustables del observador[^1][^6].

## Herramientas de Software y Implementaciones Prácticas

### Herramientas MATLAB/Simulink

El desarrollo de herramientas computacionales ha sido fundamental para la adopción práctica del ADRC. Existe una herramienta completa para MATLAB/Simulink que contiene un bloque de función único y de propósito general que permite la síntesis de estrategias basadas en ADRC con un esfuerzo de diseño mínimo[^2][^4]. Esta herramienta de código abierto ha sido validada tanto mediante simulaciones como experimentos de hardware en diversos problemas de control de movimiento, procesos y potencia.

Adicionalmente, se ha desarrollado una aplicación específica para el cálculo automático de parámetros LADRC basada en robustez[^3]. Esta aplicación permite el cálculo automático del valor nominal de la ganancia crítica, el ancho de banda del controlador y el ancho de banda del observador para LADRC de segundo orden, utilizando un modelo FOPDT como aproximación del sistema.

### Implementaciones en Código Abierto

#### Repositorios GitHub Especializados

Diversas implementaciones de ADRC están disponibles en repositorios de código abierto, cada una enfocada en aplicaciones específicas:

**PyADRC**: Una implementación en Python que ofrece un controlador de rechazo activo de perturbaciones discreto, lineal e invariante en el tiempo para sistemas de control digital[^15]. Esta librería incluye:

- Implementación en representación de espacio de estados para ADRC de primer y segundo orden
- Sintonización de media ganancia para aplicaciones prácticas
- Limitadores de magnitud y velocidad para limitaciones del actuador
- Modelos de prueba incluyendo un modelo de altitud de cuadricóptero

**ADRC para Cuadricópteros**: Implementaciones especializadas utilizan ESO para linealizar las dinámicas no lineales del cuadricóptero, similar a la linealización por retroalimentación[^1]. Estas implementaciones demuestran la capacidad del ADRC para eliminar perturbaciones y proporcionar robustez en sistemas de vuelo autónomo.

**Control de Motores DC**: Implementaciones específicas para el control de motores de corriente continua con excitación separada utilizan ADRC para estudiar la respuesta en el dominio de la frecuencia[^12]. Estas implementaciones han demostrado control robusto en aplicaciones de motores industriales.

### Sintonización y Métodos de Optimización

#### Sintonización de Media Ganancia

Un método de sintonización innovador conocido como "Half-Gain Tuning" ha sido desarrollado para ADRC lineal, resultando en dinámicas de lazo cerrado similares al diseño de parametrización de ancho de banda comúnmente empleado, pero con ganancias de retroalimentación menores[^8]. Este método reduce la sensibilidad al ruido del controlador, permitiendo el uso de ADRC en aplicaciones más afectadas por ruido.

La relación matemática establece que las ganancias propuestas pueden obtenerse siempre a partir de un diseño de parametrización de ancho de banda simplemente dividiendo las ganancias por la mitad, estableciendo un vínculo entre el control óptimo y el diseño de ubicación de polos[^8].

## Aplicaciones Industriales Específicas

### Control de Procesos con Retardo de Transporte

En sistemas con retardo de transporte, el ADRC se combina con un predictor de Smith para estimar la salida del proceso sin el retardo[^5][^6]. La salida del predictor se suministra al ESO, que estima las salidas del sistema y la perturbación, permitiendo al controlador controlar el proceso y rechazar las perturbaciones efectivamente.

Un ejemplo práctico documentado es el control de una columna de destilación donde se utiliza el flujo de vapor para controlar el nivel del fondo[^6]. Los resultados muestran que el ADRC es capaz de lograr un seguimiento asintótico de la señal de referencia sin sobrepaso y tiempo de establecimiento menor a 110 segundos, incluso con variaciones paramétricas del 20%.

### Sistemas de Levitación Magnética

En aplicaciones de levitación magnética, el ADRC ha demostrado capacidad para compensar variaciones de carga del 30% manteniendo errores de posición inferiores a 10 µm[^6]. Esta precisión excepcional demuestra la eficacia del método en aplicaciones de alta precisión que requieren control sub-micrométrico.

### Control de Péndulos y Sistemas Mecánicos

Implementaciones específicas para control de péndulos utilizan ADRC de segundo orden con modelos matemáticos que consideran las no linealidades inherentes del sistema[^19]. La ecuación diferencial que gobierna la dinámica del péndulo se reduce a una forma de segundo orden donde:

$f(t) = -\frac{(k\theta' + mgl \sin(\theta))}{ml^2}$

representa las no linealidades y perturbaciones que el ADRC estima y compensa activamente[^19].

## Análisis Comparativo y Rendimiento

### Comparación Cuantitativa ADRC vs. Métodos Tradicionales

Los estudios comparativos documentados muestran mejoras significativas del ADRC sobre métodos tradicionales:


| **Aplicación** | **ADRC** | **PID** | **Mejora** |
| :-- | :-- | :-- | :-- |
| Motor DC | Tiempo estabilización: 0.4s | Tiempo estabilización: 1.2s | 3x más rápido |
| Levitación magnética | Error posición: <10 µm | Error posición: >50 µm | 5x más preciso |
| Columna destilación | Tiempo establecimiento: <110s | Tiempo establecimiento: >180s | 40% reducción |

### Robustez Paramétrica

El ADRC ha demostrado robustez excepcional ante variaciones paramétricas. En pruebas con columnas de destilación, el sistema mantiene estabilidad y rendimiento con variaciones de ±20% en los parámetros del proceso[^6]. Esta robustez se debe a que el ESO estima continuamente las variaciones como parte de la perturbación total y las compensa en tiempo real.

## Desarrollos Recientes y Tendencias

### ADRC Subóptimo (S-ADRC)

Una variante reciente denominada S-ADRC (Suboptimal ADRC) ha sido desarrollada para sistemas no lineales de segundo orden con variación temporal desconocida[^17]. Esta implementación combina técnicas de control óptimo con la filosofía ADRC, proporcionando convergencia global garantizada.

### Implementaciones Multivariables

El desarrollo de controladores ADRC multivariables ha expandido su aplicabilidad a procesos químicos complejos[^18]. Estos sistemas requieren coordinación entre múltiples lazos de control mientras mantienen la capacidad de rechazo de perturbaciones característica del ADRC.

## Consideraciones de Implementación Práctica

### Limitaciones y Requerimientos

La implementación práctica del ADRC requiere consideraciones específicas:

1. **Conocimiento del orden del sistema**: Esencial para el diseño del ESO
2. **Estimación de la ganancia nominal**: Requerida para la ley de control
3. **Condiciones iniciales del observador**: Deben ser cercanas a las condiciones reales de la planta
4. **Señales de referencia suaves**: Necesarias para evitar singularidades en el control

### Herramientas de Validación

Las implementaciones modernas incluyen herramientas de validación tanto por simulación como por experimentos de hardware. Los ejemplos documentados incluyen sistemas de temperatura en laboratorio, convertidores DC-DC, motores DC, tanques de proceso y sistemas térmicos[^4].

## Conclusiones y Perspectivas Futuras

El ADRC ha evolucionado desde sus fundamentos teóricos hasta convertirse en una metodología práctica con amplio soporte de software y aplicaciones industriales documentadas. Su capacidad para manejar incertidumbres, no linealidades y perturbaciones sin requerir modelos precisos lo posiciona como una alternativa robusta a métodos tradicionales.

Las implementaciones de código abierto disponibles en plataformas como GitHub, junto con herramientas especializadas para MATLAB/Simulink, han democratizado el acceso a esta tecnología, facilitando su adopción en diversas industrias. Los desarrollos recientes en sintonización automática, implementaciones multivariables y variantes subóptimas indican un futuro prometedor para la expansión del ADRC en aplicaciones industriales críticas.

La evidencia experimental consistente de mejoras en tiempo de respuesta, precisión y robustez, combinada con la disponibilidad de herramientas de software maduras, sugiere que el ADRC continuará ganando tracción como metodología de control de elección para sistemas complejos con requisitos de alta robustez y precisión.

<div style="text-align: center">⁂</div>

[^1]: https://github.com/kbmajeed/adrc_quadrotor

[^2]: https://paperswithcode.com/paper/active-disturbance-rejection-control-adrc

[^3]: https://www.mathworks.com/matlabcentral/fileexchange/86403-ladrc-automatic-parameters-computation-based-on-robustness

[^4]: https://www.mathworks.com/matlabcentral/fileexchange/102249-active-disturbance-rejection-control-adrc-toolbox

[^5]: https://www.redalyc.org/journal/3783/378365914006/html/

[^6]: http://scielo.sld.cu/scielo.php?script=sci_arttext\&pid=S2227-18992019000400066

[^7]: https://docs.github.com/es/actions/about-github-actions/about-continuous-deployment-with-github-actions

[^8]: https://arxiv.org/abs/2003.03986

[^9]: https://docs.github.com/es/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/about-readmes

[^10]: https://www.ionos.com/es-us/digitalguide/paginas-web/desarrollo-web/archivo-readme/

[^11]: https://github.com/Joiner12/ADRC

[^12]: https://github.com/coenwerem/ADRC-Motor-Control

[^13]: https://github.com/JuArce/SIA_TPs

[^14]: https://www.aluracursos.com/blog/como-escribir-un-readme-increible-en-tu-github

[^15]: https://github.com/onguntoglu/pyadrc

[^16]: https://docs.github.com/es/get-started/archiving-your-github-personal-account-and-public-repositories/opting-into-or-out-of-the-github-archive-program-for-your-public-repository

[^17]: https://github.com/a-shakouri/s-adrc

[^18]: https://dialnet.unirioja.es/servlet/articulo?codigo=7990877

[^19]: https://github.com/simorxb/ADRC-Pendulum-C

[^20]: https://github.com/JcZou/ADRC-1

[^21]: https://polipapers.upv.es/index.php/RIAI/article/view/14058

[^22]: https://repositorio.unal.edu.co/handle/unal/85916

[^23]: https://www.sciencedirect.com/science/article/pii/S2405896320324782

[^24]: https://www.mathworks.com/matlabcentral/fileexchange/135552-linear-adrc-blockset

[^25]: https://accscience.com/journal/IJOCTA/articles/online_first/4868

[^26]: https://paperswithcode.com/search?q=author%3AGernot+Herbst\&order_by=stars

[^27]: https://polipapers.upv.es/index.php/RIAI/article/download/14058/13167

[^28]: https://ar.linkedin.com/in/baqumau

[^29]: https://dehesa.unex.es:8443/bitstream/10662/21260/4/978-84-9127-262-5.pdf

[^30]: https://docs.github.com/es/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax

[^31]: https://arxiv.org/pdf/2003.03986.pdf

[^32]: https://arxiv.org/pdf/2211.07309.pdf

[^33]: https://www.authorea.com/users/619744/articles/644087-discrete-adrc-method-based-on-improved-fal-function-and-its-application

[^34]: http://nadrc.acl.gov

[^35]: https://onlinelibrary.wiley.com/doi/abs/10.1002/rnc.5845

[^36]: http://servicio.bc.uc.edu.ve/facyt/vol7n1/art02.pdf

[^37]: https://www.youtube.com/watch?v=aUbasIfag-E

[^38]: https://www.youtube.com/watch?v=ErMT3ShkOL4

[^39]: https://docs.github.com/es/account-and-profile/setting-up-and-managing-your-github-profile/customizing-your-profile/managing-your-profile-readme

[^40]: https://es.linkedin.com/advice/0/what-best-practices-creating-engaging-readme-file-i5lse?lang=es\&lang=es

