# Perfiles de Movimiento
Para la clase de hoy se presenta el tema de perfiles de movimiento, los cuales describe cómo cambian la posición, velocidad y aceleración de un objeto durante un determinado intervalo de tiempo, vemos algunos ejemplos y ejercicios que sirven para profundizar sobre el tema y su aplicabilidad en control de movimiento.

## 1. ¿Qué son perfiles de Movimiento?
>🔑 *Perfiles de Movimiento:*  Un perfil de movimiento es la descripción técnica de cómo varían en el tiempo la posición, la velocidad y la aceleración de un eje u objeto, asegurando transiciones suaves entre fases de aceleración, velocidad constante y desaceleración.

![erich1](https://github.com/user-attachments/assets/e0894bbd-cfd1-42ab-aeb1-f3e3c62883a5)

Figura 1. Perfil de movimiento.

Un perfil de movimiento establece la ruta que un punto debe seguir desde el punto “A” hasta el punto “B”, describiendo en cada fase cómo evolucionan su posición, velocidad y aceleración. En el caso más sencillo, con un único eje, esta trayectoria es una línea recta. Para operaciones más complejas se sincronizan varios ejes y se combinan distintos subperfiles, de modo que, al integrarse, realicen la tarea deseada. De este modo, cada subperfil no solo define la geometría del recorrido, sino también las fases de aceleración, velocidad constante y desaceleración en cada eje, asegurando movimientos precisos, fluidos y sin vibraciones.

## 2. Cinematica

En el estudio y diseño de perfiles de movimiento, la cinemática es fundamental, ya que proporciona las herramientas necesarias para describir con precisión cómo se desplaza un objeto en función del tiempo. Esta rama de la física se enfoca exclusivamente en el cómo del movimiento, sin tener en cuenta las fuerzas que lo generan. Su análisis se basa en tres conceptos esenciales: posición, velocidad y aceleración, los cuales están directamente relacionados entre sí a través de derivadas e integrales.


>🔑 *Posición:* $$s(t)$$ es la función de posición: nos dice exactamente dónde está el objeto en el instante t. En su forma integral es $$s = \int v(t)\,dt$$
>
>🔑 *Velocidad:* $$v(t) = \frac{ds}{dt}$$ es la velocidad: calcula la pendiente de s(t), es decir, cuánto y con qué dirección cambia la posición por unidad de tiempo. En su forma integral es $$v = \int a(t)\,dt$$
>
>🔑 *Aceleración:* $$a(t) = \dfrac{dv}{dt}$$ es la aceleración: mide la variación de la velocidad en el tiempo, o sea, cómo de rápido aumenta o disminuye la velocidad.  

## Reglas Geometricas

$$
v = v_0 + a(t - t_0)
$$

$$
s = s_0 + \frac{1}{2}(t - t_0)\left(v_0 + a(t - t_0)\right)
$$

💡**Ejemplo 1:**

Encuentre la posición y la aceleración en t=5 s

R:// La aceleración sería la pendiente de la velocidad: $$a = \frac{10}{5} \\ = 2\text{in}/s^2$$ , mientras que el área bajo la curva de velocidad es hasta t=5 s es la posición alcanzada en t=5 s $$s = \frac{1}{2}(10 \cdot 5) = 25\, \text{in/s}$$


💡**Ejemplo 2:**

Un eje está viajando a una velocidad de 10 cm/s. En t=5 s empieza a disminuir la velocidad como se ve en el perfil. Cual es la posición del eje cuando se detiene? Asuma que empieza a desacelerar a 25 cm

R:// La pendiente de la velocidad es la aceleración: $$a = \frac{-10\ \text{cm/s} \cdot \frac{1\ \text{m}}{100\ \text{cm}}}{15\ \text{s} - 5\ \text{s}} = \frac{-0.1\ \text{m/s}}{10\ \text{s}} \\ = -0.01\ \text{m/s}^2$$ , mientras que el área del perfil de velocidad
triangular es la posición alcanzada en t=15 s, $$S_0 = \frac{1}{2} \cdot (15\,\text{s} - 5\,\text{s}) \cdot 0{,}1\,\frac{\text{m}}{\text{s}} = 0{,}5\,\text{m}$$

## 3. Perfiles de Movimiento Trapezoidal

Un perfil de movimiento trapezoidal es una forma bastante común de controlar cómo se mueve un objeto, como el eje de un robot o una máquina. Se divide en tres etapas claras: la primera es que el objeto acelera de forma constante, luego mantiene una velocidad fija durante un tiempo y finalmente, desacelera también de manera constante hasta detenerse. Si dibujamos la velocidad a lo largo del tiempo, el gráfico toma forma de trapecio, de ahí su nombre. Este tipo de perfil es útil porque ayuda a que el movimiento sea fluido y eficiente, sin exigirle demasiado al motor o sistema, respetando los límites de aceleración que se pueden manejar con seguridad. Una de las razones por las que se usa tanto este perfil es que es fácil de calcular y lo suficientemente preciso para muchas tareas industriales. Aunque no es tan suave como un perfil en "S", que reduce aún más los cambios bruscos de aceleración, el perfil trapezoidal ofrece un buen equilibrio entre velocidad, control y facilidad de implementación. Es ideal cuando se necesita mover algo rápido y de forma repetitiva, como en impresoras 3D, máquinas CNC o sistemas automatizados de producción.

Las principales caracteristicas del perfil trapezoidal son:

- **Forma del perfil:**  
  Tiene forma de trapecio en la gráfica de velocidad vs. tiempo.

- **Fases del movimiento:**  
  1. Aceleración constante  
  2. Velocidad constante  
  3. Desaceleración constante

- **Nivel de suavidad:**  
  Es un perfil moderadamente suave. Más suave que una aceleración instantánea, pero menos suave que un perfil en "S".

- **Facilidad de cálculo:**  
  Se basa en fórmulas básicas de cinemática, por lo que es fácil de implementar.

- **Tiempo total del movimiento:**  
  Se reparte entre las tres fases (aceleración, velocidad constante y desaceleración).

- **Ventajas:**  
  - Fácil de implementar  
  - Eficiente  
  - Buen equilibrio entre rapidez y control  
  - Ideal para movimientos repetitivos

- **Limitaciones:**  
  - Cambios bruscos en la aceleración pueden generar vibraciones o mayor desgaste mecánico

- **Aplicaciones comunes:**  
  - Robótica  
  - Impresoras 3D  
  - Máquinas CNC  
  - Sistemas de automatización industrial

💡**Ejemplo 3:**

El eje X de un robot Gantry debe moverse una distancia de 10 cm. La aceleración máxima permitida en este eje es de 1 cm/s², y se desea mover el eje a una velocidad máxima de 2 cm/s. cuanto tiempo tomará hacer este movimiento

$$
t_a = t_d = \frac{v_m}{a} = \frac{2\ \text{cm/s}}{1\ \text{cm/s}^2} = 2\ \text{s}
$$

$$
t_m = \frac{L}{v_m} - t_a = \frac{10\ \text{cm}}{2\ \text{cm/s}} - 2\ \text{s} = 3\ \text{s}
$$

$$
t_{\text{total}} = t_a + t_m + t_d = 2 + 3 + 2 = 7\ \text{s}
$$

![erich2](https://github.com/user-attachments/assets/6d61cdd9-47b5-4629-a93b-ce1cb5dafdf8)

Figura 2. Perfil de movimiento Robot Gantry.

## 4. Ejercicios

### 📚Ejercicio 1:
Un eje (axis) lineal comienza su movimiento desde el reposo en la posición 0, con una aceleración de 2 m/s2. Después de moverse durante 5 s, cual es la posición del eje (axis)?

- Posición inicial: $$\( s_0 = 0\ \text{m} \)$$  
- Velocidad inicial: $$\( v_0 = 0\ \text{m/s} \)$$
- Aceleración: $$\( a = 2\ \text{m/s}^2 \)$$  
- Tiempo: $$\( t = 5\ \text{s} \)$$
  
$$
s = s_0 + \frac{1}{2} a t^2
$$

$$
s = 0 + \frac{1}{2}(2)(5^2) = \frac{1}{2} \cdot 2 \cdot 25 = 25\ \text{m}
$$

La posición del eje después de 5 segundos es $$\boxed{25\ \text{m}}$$

### 📚Ejercicio 2:

Dado el perfil de velocidad de la figura,calcule 𝑠𝐴, 𝑠𝐵, 𝑠𝐶 usando las reglas geométricas y el método analítico del perfil de movimiento.

![image](https://github.com/user-attachments/assets/626782a4-5e51-4b8e-ac0c-d2ece58fd3d8)


## 5. Conclusiones

- El diseño de perfiles de movimiento eficientes es fundamental para optimizar la precisión y el tiempo de ciclo en sistemas automatizados, porque en industrias como la manufactura avanzada y la robótica, usar perfiles como el trapezoidal o el perfil en S permite movimientos suaves y controlados que reducen el desgaste mecánico y aumentan la vida útil de los componentes.

- El entendimiento de los conceptos básicos de cinemática (posición, velocidad y aceleración) permite diseñar trayectorias predecibles y seguras, esto es clave en sistemas donde el movimiento interactúa con humanos o procesos sensibles como de ensamble fino o corte de alta precisión.

- El control digital facilita la implementación práctica de perfiles de movimiento complejos mediante algoritmos en microcontroladores, PLCs y sistemas embebidos, debido al procesamiento digital, se pueden integrar sensores y retroalimentación para ajustar dinámicamente los perfiles de movimiento en tiempo real.

- La correcta selección del perfil de movimiento depende del tipo de aplicación: perfiles trapezoidales para movimientos rápidos y repetitivos; perfiles en S para suavidad y menor impacto, esto permite adaptar soluciones a sectores diversos como la industria alimentaria, farmacéutica, automotriz, textil o aeroespacial.

- Integrar el control de movimiento dentro de sistemas de automatización más amplios mejora la eficiencia global de la línea de producción porque a través de protocolos industriales, interfaces digitales y control distribuido, los perfiles de movimiento pueden sincronizarse con visión artificial, sensores de carga o control de calidad automatizado.

## 6. Referencias
[1] R. Kelly, V. Santibáñez, and A. Loria, Control of Robot Manipulators in Joint Space, Springer, 2005
[2] K. J. Åström and R. M. Murray, Feedback Systems: An Introduction for Scientists and Engineers, Princeton University Press, 2008.
[3] H. Goldstein, C. Poole, and J. Safko, Classical Mechanics, 3rd ed. San Francisco, CA, USA: Addison-Wesley, 2002.
[4] M. Alonso and E. J. Finn, Fundamental University Physics: Volume 1 - Mechanics, 2nd ed. Reading, MA, USA: Addison-Wesley, 1973
[5] K. Ogata, Discrete-Time Control Systems, 2nd ed. Upper Saddle River, NJ, USA: Prentice Hall, 1995.
[6] M. Gopal, Digital Control and State Variable Methods, 4th ed. New Delhi, India: McGraw-Hill Education, 2012.
