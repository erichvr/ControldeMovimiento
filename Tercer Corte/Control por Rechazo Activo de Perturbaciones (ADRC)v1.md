# Control por Rechazo Activo de Perturbaciones (ADRC)

El Control por Rechazo Activo de Perturbaciones (ADRC) representa un modelo moderno en ingeniería de control que ha experimentado un desarrollo significativo tanto en sus fundamentos teóricos como en sus implementaciones prácticas. Esta metodología, originalmente propuesta por Jingqing Han en los años 1990, se ha consolidado como una solución robusta para sistemas con dinámicas complejas, ofreciendo ventajas frente a otros métodos en escenarios con perturbaciones variables y modelado impreciso. Se enfoca en tratar todas las incertidumbres como una "perturbación total" que puede ser estimada y compensada en tiempo real.

## 1. Fundamentos Teóricos del ADRC

El ADRC se basa en una filosofía distinta a las técnicas de control convencionales. En lugar de depender de un modelo matemático preciso del sistema a controlar, el ADRC trata de estimar y compensar todas las incertidumbres, no linealidades y perturbaciones del sistema en tiempo real. Esta aproximación permite simplificar sistemas complejos y proporcionar un control robusto incluso con conocimiento limitado de la planta.

>🔑 *Control por Rechazo Activo de Perturbaciones (ADRC)*: metodología de control que estima y compensa en tiempo real las perturbaciones e incertidumbres del sistema, permitiendo un control robusto sin requerir un modelo matemático preciso de la planta.

>🔑 *Perturbación total*: concepto que unifica todas las incertidumbres del sistema (no linealidades, perturbaciones externas, errores de modelado) en una única variable que puede ser estimada y compensada en tiempo real.

La arquitectura básica del ADRC consta de tres componentes principales que trabajan de manera coordinada:

1. **Mecanismo de seguimiento de trayectoria (TD)**: Genera señales de referencia suaves y diferenciables
2. **Observador de Estado Extendido (ESO)**: Estima tanto los estados del sistema como la perturbación total
3. **Ley de control no lineal (NLSEF)**: Compensa activamente las perturbaciones estimadas

## 2. Arquitectura y Componentes Fundamentales

La implementación del ADRC requiere comprender profundamente cada uno de sus componentes y cómo interactúan entre sí para proporcionar un control robusto y efectivo.

>🔑 *Observador de Estado Extendido (ESO)*: componente fundamental del ADRC que estima los estados del sistema y la perturbación total, considerando esta última como un estado adicional (extendido) del sistema.

>🔑 *Mecanismo de seguimiento de trayectoria (TD)*: generador de perfiles de referencia que produce señales suaves para evitar discontinuidades en el control.

### 2.1. Observador de Estado Extendido (ESO)

El ESO es el corazón del ADRC. Para un sistema de segundo orden, el ESO se define mediante el siguiente sistema de ecuaciones:

$$
\begin{cases} 
\dot{z}_1 = z_2 + \beta_1 e \\ 
\dot{z}_2 = z_3 + b_0 u + \beta_2 e \\ 
\dot{z}_3 = \beta_3 e
\end{cases}
$$

Donde:
- $z_1, z_2$ son las estimaciones de los estados del sistema
- $z_3$ es la estimación de la perturbación total
- $e = y - z_1$ representa el error de estimación
- $\beta_i$ son las ganancias ajustables del observador
- $b_0$ es una estimación de la ganancia de entrada del sistema
- $u$ es la señal de control

### 2.2. Ley de Control No Lineal (NLSEF)

La ley de control no lineal utiliza las estimaciones del ESO para compensar las perturbaciones y asegurar que el sistema siga la referencia deseada. La ley de control básica se expresa como:

$$u = \frac{u_0 - z_3}{b_0}$$

Donde $u_0$ es la señal de control calculada por un controlador PD o función de error no lineal (NLSEF):

$$u_0 = k_p(r - z_1) + k_d(r' - z_2)$$

## 3. Implementaciones Prácticas y Herramientas

El ADRC ha sido implementado en diversas plataformas y con distintas herramientas que facilitan su aplicación en problemas reales de control.

### 3.1. Herramientas MATLAB/Simulink

Existen varias herramientas que facilitan la implementación del ADRC en entornos de simulación y desarrollo:

1. **ADRC Toolbox**: Herramienta completa para MATLAB/Simulink que contiene bloques de función para la síntesis de estrategias basadas en ADRC con mínimo esfuerzo de diseño.

2. **LADRC Automatic Parameters Computation**: Aplicación para el cálculo automático de parámetros LADRC basada en robustez.


### 3.2. Implementaciones en Código Abierto

Diversas implementaciones de ADRC están disponibles en repositorios de código abierto, cada una enfocada en aplicaciones específicas:

1. **PyADRC**: Implementación en Python que ofrece un controlador ADRC discreto, lineal e invariante en el tiempo para sistemas de control digital.

2. **ADRC para Cuadricópteros**: Implementaciones especializadas que utilizan ESO para linealizar las dinámicas no lineales de vehículos aéreos.

## 4. Métodos de Sintonización

La sintonización adecuada de los parámetros del ADRC es crucial para obtener un rendimiento óptimo en aplicaciones prácticas.

>🔑 *Sintonización de ancho de banda*: método tradicional para ajustar los parámetros del ADRC basado en la selección de un ancho de banda del controlador ($\omega_c$) y un ancho de banda del observador ($\omega_o$).

### 4.1. Sintonización de Media Ganancia

Un método innovador conocido como "Half-Gain Tuning" (Sintonización de Media Ganancia) ha sido desarrollado para ADRC lineal, resultando en dinámicas de lazo cerrado similares al diseño de parametrización de ancho de banda, pero con ganancias de retroalimentación menores.

$$\beta_1 = \frac{3\omega_o}{2}, \beta_2 = \frac{3\omega_o^2}{2}, \beta_3 = \frac{\omega_o^3}{2}$$

💡**Ejemplo 2:** Comparación entre sintonización tradicional y sintonización de media ganancia para un sistema de segundo orden:

| **Método** | **$\beta_1$** | **$\beta_2$** | **$\beta_3$** | **Sensibilidad al ruido** |
|------------|---------------|---------------|---------------|---------------------------|
| Tradicional | $3\omega_o$ | $3\omega_o^2$ | $\omega_o^3$ | Alta |
| Media Ganancia | $\frac{3\omega_o}{2}$ | $\frac{3\omega_o^2}{2}$ | $\frac{\omega_o^3}{2}$ | Reducida |

Tabla 1. Comparación de métodos de sintonización para ESO de segundo orden

## 5. Aplicaciones Industriales

El ADRC ha demostrado su eficacia en numerosas aplicaciones industriales donde los métodos tradicionales enfrentan limitaciones debido a dinámicas complejas o perturbaciones variables.

### 5.1. Control de Procesos con Retardo de Transporte

En sistemas con retardo de transporte, el ADRC se combina con un predictor de Smith para estimar la salida del proceso sin el retardo. La salida del predictor se suministra al ESO, que estima las salidas del sistema y la perturbación.

![Diagrama de ADRC con predictor de Smith](images/adrc/ques de ADRC con predictor de Smith para sistemas con retardo

### 5.2. Sistemas de Levitación Magnética

En aplicaciones de levitación magnética, el ADRC ha demostrado capacidad para compensar variaciones de carga del 30% manteniendo errores de posición inferiores a 10 µm. La ecuación que describe la dinámica del sistema de levitación es:

$$m\ddot{x} = mg - \frac{ki^2}{x^2}$$

Donde:
- $m$ es la masa del objeto levitado
- $x$ es la posición
- $g$ es la aceleración de la gravedad
- $k$ es una constante electromagnética
- $i$ es la corriente en el electroimán

### 5.3. Control de Motores y Sistemas Mecánicos

Implementaciones específicas para control de motores DC utilizan ADRC para estudiar la respuesta en el dominio de la frecuencia. La ecuación que modela un motor DC es:

$$J\ddot{\theta} + B\dot{\theta} = K_t i$$

Donde:
- $J$ es el momento de inercia
- $\theta$ es la posición angular
- $B$ es el coeficiente de fricción
- $K_t$ es la constante de torque
- $i$ es la corriente de armadura

## 6. Análisis Comparativo y Rendimiento

Los estudios comparativos documentados muestran mejoras significativas del ADRC sobre métodos tradicionales de control como el PID.

| **Aplicación** | **ADRC** | **PID** | **Mejora** |
|----------------|----------|---------|------------|
| Motor DC | Tiempo estabilización: 0.4s | Tiempo estabilización: 1.2s | 3x más rápido |
| Levitación magnética | Error posición: 🔑 *ADRC Lineal (LADRC)*: simplificación del ADRC original que utiliza relaciones lineales en el observador y el controlador, facilitando el análisis y la implementación.

>🔑 *ADRC Subóptimo (S-ADRC)*: variante que combina técnicas de control óptimo con la filosofía ADRC, proporcionando convergencia global garantizada para sistemas no lineales.

### 7.1. ADRC Multivariable

El desarrollo de controladores ADRC multivariables ha expandido su aplicabilidad a procesos complejos con múltiples entradas y salidas. Estos sistemas requieren coordinación entre múltiples lazos de control mientras mantienen la capacidad de rechazo de perturbaciones.

![Diagrama ADRC multivariloques de un sistema ADRC multivariable para un proceso con múltiples entradas y salidas

## 8. Consideraciones de Implementación Práctica

La implementación práctica del ADRC requiere consideraciones específicas para garantizar un rendimiento óptimo.

1. **Conocimiento del orden del sistema**: Esencial para el diseño del ESO
2. **Estimación de la ganancia nominal**: Requerida para la ley de control
3. **Condiciones iniciales del observador**: Deben ser cercanas a las condiciones reales de la planta
4. **Señales de referencia suaves**: Necesarias para evitar singularidades en el control

💡**Ejemplo 3:** Implementación discreta del ESO para un sistema de segundo orden con período de muestreo $T$:

```matlab
% Implementación discreta del ESO
function z_next = ESO_discreto(z, y, u, b0, beta, T)
    % z: estado actual del observador [z1; z2; z3]
    % y: salida medida del sistema
    % u: señal de control
    % b0: ganancia nominal
    % beta: ganancias del observador [beta1; beta2; beta3]
    % T: período de muestreo
    
    % Error de estimación
    e = y - z(1);
    
    % Actualización del observador (método de Euler)
    z_next = zeros(3,1);
    z_next(1) = z(1) + T*(z(2) + beta(1)*e);
    z_next(2) = z(2) + T*(z(3) + b0*u + beta(2)*e);
    z_next(3) = z(3) + T*beta(3)*e;
    
    return z_next;
end
```

# Ejercicios

## 📚 Ejercicio 1
Diseñar un controlador ADRC de segundo orden para un motor DC cuya función de transferencia es:

$$G(s) = \frac{10}{s^2 + 2s + 10}$$

a) Determine los parámetros del ESO utilizando el método de sintonización de ancho de banda con $\omega_c = 10$ rad/s y $\omega_o = 30$ rad/s.
b) Implemente el controlador ADRC en código MATLAB y compare su respuesta con un controlador PID convencional ante una entrada escalón y una perturbación constante.

### Solución:

a) Para un sistema de segundo orden, los parámetros del ESO son:

Usando el método de sintonización de ancho de banda con $\omega_o = 30$ rad/s:
- $\beta_1 = 3\omega_o = 3 \times 30 = 90$
- $\beta_2 = 3\omega_o^2 = 3 \times 30^2 = 2700$
- $\beta_3 = \omega_o^3 = 30^3 = 27000$

Para el controlador:
- $k_p = \omega_c^2 = 10^2 = 100$
- $k_d = 2\omega_c = 2 \times 10 = 20$

La ganancia nominal $b_0 = 10$ (del término independiente de la función de transferencia).

b) Implementación en MATLAB:

```matlab
% Parámetros del sistema
b0 = 10;  % Ganancia nominal
A = [0 1; -10 -2];  % Matriz de estado del sistema
B = [0; 10];        % Matriz de entrada
C = [1 0];          % Matriz de salida

% Parámetros del ADRC
wc = 10;            % Ancho de banda del controlador
wo = 30;            % Ancho de banda del observador
beta1 = 3*wo;
beta2 = 3*wo^2;
beta3 = wo^3;
kp = wc^2;
kd = 2*wc;

% Simulación
dt = 0.001;         % Paso de tiempo
Tfinal = 2;         % Tiempo final de simulación
t = 0:dt:Tfinal;    % Vector de tiempo
n = length(t);      % Número de muestras

% Inicialización
x = zeros(2,n);     % Estados del sistema
z = zeros(3,n);     % Estados del observador
y = zeros(1,n);     % Salida del sistema
u_adrc = zeros(1,n); % Control ADRC
r = ones(1,n);      % Referencia (escalón unitario)
r_dot = zeros(1,n); % Derivada de la referencia

% Perturbación (aplicada en t=1s)
d = zeros(1,n);
d(t>=1) = 2;        % Perturbación constante de amplitud 2

% Simulación del sistema con ADRC
for i = 1:n-1
    % Salida del sistema
    y(i) = C * x(:,i);
    
    % Error de estimación
    e = y(i) - z(1,i);
    
    % Actualización del ESO
    z(1,i+1) = z(1,i) + dt*(z(2,i) + beta1*e);
    z(2,i+1) = z(2,i) + dt*(z(3,i) + b0*u_adrc(i) + beta2*e);
    z(3,i+1) = z(3,i) + dt*(beta3*e);
    
    % Ley de control ADRC
    u0 = kp*(r(i) - z(1,i)) + kd*(r_dot(i) - z(2,i));
    u_adrc(i+1) = (u0 - z(3,i))/b0;
    
    % Actualización del sistema (con perturbación)
    dx = A*x(:,i) + B*u_adrc(i) + [0; d(i)];
    x(:,i+1) = x(:,i) + dt*dx;
end
y(n) = C * x(:,n);  % Última salida

% Diseño del controlador PID para comparación
Kp = 5;
Ki = 10;
Kd = 0.5;

% Inicialización para simulación con PID
x_pid = zeros(2,n);
y_pid = zeros(1,n);
u_pid = zeros(1,n);
e_pid = zeros(1,n);
e_pid_int = 0;
e_pid_prev = 0;

% Simulación del sistema con PID
for i = 1:n-1
    % Salida del sistema
    y_pid(i) = C * x_pid(:,i);
    
    % Error
    e_pid(i) = r(i) - y_pid(i);
    
    % Integración del error
    e_pid_int = e_pid_int + e_pid(i)*dt;
    
    % Derivada del error
    if i > 1
        e_pid_dot = (e_pid(i) - e_pid_prev)/dt;
    else
        e_pid_dot = 0;
    end
    e_pid_prev = e_pid(i);
    
    % Ley de control PID
    u_pid(i) = Kp*e_pid(i) + Ki*e_pid_int + Kd*e_pid_dot;
    
    % Actualización del sistema (con perturbación)
    dx = A*x_pid(:,i) + B*u_pid(i) + [0; d(i)];
    x_pid(:,i+1) = x_pid(:,i) + dt*dx;
end
y_pid(n) = C * x_pid(:,n);  % Última salida

% Gráficos de comparación
figure;
subplot(2,1,1);
plot(t, r, 'k--', t, y, 'b-', t, y_pid, 'r-');
legend('Referencia', 'ADRC', 'PID');
title('Respuesta del sistema ante entrada escalón y perturbación');
xlabel('Tiempo (s)');
ylabel('Salida');
grid on;

subplot(2,1,2);
plot(t, u_adrc, 'b-', t, u_pid, 'r-');
legend('Control ADRC', 'Control PID');
title('Señales de control');
xlabel('Tiempo (s)');
ylabel('Control');
grid on;
```

El resultado muestra que el controlador ADRC tiene una respuesta más rápida y rechaza mejor las perturbaciones que el controlador PID. El ADRC mantiene la salida cerca de la referencia incluso después de aplicar la perturbación en t=1s, mientras que el PID muestra una desviación notable antes de corregirla.

## 📚 Ejercicio 2
Para un sistema de levitación magnética descrito por la ecuación no lineal:

$$m\ddot{x} = mg - \frac{ki^2}{x^2}$$

Donde $m=0.1$ kg, $g=9.8$ m/s², $k=10^{-4}$ N·m²/A², $x$ es la posición (m) e $i$ es la corriente (A), diseñe un controlador ADRC que mantenga la posición en $x_0=0.01$ m.

a) Linealice el sistema alrededor del punto de operación $x_0=0.01$ m e $i_0=1$ A.
b) Determine los parámetros del controlador ADRC considerando que el sistema linealizado es de segundo orden.
c) Describa cómo implementaría el ESO para estimar las no linealidades y perturbaciones del sistema.

### Solución:

a) Linealización del sistema:

Primero, calculamos la corriente de equilibrio $i_0$ para la posición $x_0=0.01$ m:
En equilibrio, $m\ddot{x} = 0$, por lo que:
$mg - \frac{ki_0^2}{x_0^2} = 0$
$i_0^2 = \frac{mgx_0^2}{k} = \frac{0.1 \times 9.8 \times 0.01^2}{10^{-4}} = 0.098$
$i_0 = 0.313$ A

Linealización alrededor del punto de operación $(x_0, i_0)$:
$\delta\ddot{x} = \frac{2ki_0^2}{x_0^3}\delta x - \frac{2ki_0}{x_0^2}\delta i$

Calculando los coeficientes:
$a = \frac{2ki_0^2}{x_0^3} = \frac{2 \times 10^{-4} \times 0.313^2}{0.01^3} = 196$
$b = -\frac{2ki_0}{x_0^2} = -\frac{2 \times 10^{-4} \times 0.313}{0.01^2} = -0.626$

El sistema linealizado queda:
$\delta\ddot{x} = 196\delta x - 0.626\delta i$

Reescribiéndolo en forma estándar:
$\delta\ddot{x} - 196\delta x = -0.626\delta i$
$\delta\ddot{x} = 196\delta x + 0.626\delta i$

b) Parámetros del controlador ADRC:

Para el sistema linealizado, la ganancia nominal es $b_0 = 0.626$.

Seleccionamos un ancho de banda del controlador $\omega_c = 15$ rad/s y un ancho de banda del observador $\omega_o = 45$ rad/s (3 veces $\omega_c$).

Parámetros del ESO:
- $\beta_1 = 3\omega_o = 3 \times 45 = 135$
- $\beta_2 = 3\omega_o^2 = 3 \times 45^2 = 6075$
- $\beta_3 = \omega_o^3 = 45^3 = 91125$

Parámetros del controlador:
- $k_p = \omega_c^2 = 15^2 = 225$
- $k_d = 2\omega_c = 2 \times 15 = 30$

c) Implementación del ESO:

Para el sistema de levitación magnética, el ESO estimaría tanto los estados del sistema como las no linealidades y perturbaciones. La implementación sería:

1. Definir el sistema en la forma estándar:
   $\ddot{x} = f(x, \dot{x}, d) + b_0 u$
   
   Donde $f(x, \dot{x}, d)$ representa todas las dinámicas desconocidas, no linealidades y perturbaciones, y $b_0$ es la ganancia nominal.

2. Diseñar el ESO:
   
   $$
   \begin{cases} 
   \dot{z}_1 = z_2 + \beta_1 e \\ 
   \dot{z}_2 = z_3 + b_0 u + \beta_2 e \\ 
   \dot{z}_3 = \beta_3 e
   \end{cases}
   $$
   
   Donde $e = x - z_1$ es el error de estimación.

3. Implementar la ley de control:
   
   $$u = \frac{u_0 - z_3}{b_0}$$
   
   Donde $u_0 = k_p(r - z_1) + k_d(r' - z_2)$, con $r$ como la posición de referencia.

Para este sistema específico, el ESO estimaría la dinámica no lineal $mg - \frac{ki^2}{x^2}$ como parte del término de perturbación $z_3$, permitiendo su compensación en tiempo real sin necesidad de un modelo matemático preciso.

## 10. Conclusiones

El Control por Rechazo Activo de Perturbaciones (ADRC) representa un paradigma innovador en la ingeniería de control que ofrece soluciones robustas para sistemas complejos. A diferencia de los métodos tradicionales que dependen de modelos matemáticos precisos, el ADRC estima y compensa las perturbaciones en tiempo real, simplificando significativamente el proceso de diseño y mejorando el rendimiento del sistema.

Los fundamentos teóricos del ADRC, basados en el concepto de "perturbación total" y el Observador de Estado Extendido (ESO), proporcionan una base sólida para su implementación en diversas aplicaciones industriales. Las herramientas de software disponibles, tanto en MATLAB/Simulink como en implementaciones de código abierto, facilitan su aplicación práctica.

Los métodos de sintonización, especialmente la innovadora "Sintonización de Media Ganancia", permiten optimizar el rendimiento del ADRC reduciendo su sensibilidad al ruido. Las aplicaciones industriales demuestran su eficacia en sistemas con retardo, levitación magnética y control de motores, superando consistentemente a los métodos tradicionales en términos de velocidad de respuesta, precisión y robustez.

El ADRC continúa evolucionando con variantes como el LADRC, S-ADRC y ADRC multivariable, expandiendo su aplicabilidad a una gama más amplia de problemas de control. Con su capacidad para manejar sistemas complejos con incertidumbres y perturbaciones, el ADRC se posiciona como una metodología de control de vanguardia para los desafíos de la automatización moderna.

## 11. Referencias

1. Han, J. (2009). "From PID to Active Disturbance Rejection Control". IEEE Transactions on Industrial Electronics, 56(3), 900-906.

2. Gao, Z. (2006). "Active Disturbance Rejection Control: A Paradigm Shift in Feedback Control System Design". American Control Conference.

3. Herbst, G. (2013). "A Simulative Study on Active Disturbance Rejection Control (ADRC) as a Control Tool for Practitioners". Electronics, 2(3), 246-279.

4. Huang, Y., & Xue, W. (2014). "Active Disturbance Rejection Control: Methodology and Theoretical Analysis". ISA Transactions, 53(4), 963-976.

5. Madoński, R., & Herman, P. (2011). "Survey on methods of increasing the efficiency of extended state disturbance observers". ISA Transactions, 50(2), 217-226.

6. Zheng, Q., & Gao, Z. (2018). "On practical applications of active disturbance rejection control". Proceedings of the 29th Chinese Control and Decision Conference (CCDC).
