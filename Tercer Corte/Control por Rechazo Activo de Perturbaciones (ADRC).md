# Control por Rechazo Activo de Perturbaciones (ADRC): Fundamentos y Aplicaciones

El Control por Rechazo Activo de Perturbaciones (ADRC) representa un paradigma moderno en ingeniería de control, destacándose por su capacidad para manejar sistemas con dinámicas complejas y desconocidas. Este enfoque integra técnicas avanzadas de observación de estados y compensación no lineal, ofreciendo ventajas significativas frente a métodos tradicionales como el PID en escenarios con perturbaciones variables y modelado impreciso[1][3].

## 1. Principios Básicos del ADRC

### 1.1. Filosofía del Rechazo Activo
El ADRC unifica todas las incertidumbres del sistema (no linealidades, perturbaciones externas, errores de modelado) en una única "perturbación total" ($$f$$). Esta se estima mediante un Observador de Estado Extendido (ESO) y se compensa en tiempo real, transformando el sistema en una forma canónica simplificada[1][3].

>🔑 *Definición:* El Observador de Estado Extendido (ESO) es un componente crítico del ADRC que expande el vector de estados para incluir la perturbación total como variable de estado adicional, permitiendo su estimación y cancelación activa.

## 2. Componentes Clave del ADRC

### 2.1. Arquitectura del Sistema
El ADRC consta de tres elementos fundamentales:
1. Mecanismo de seguimiento de trayectoria (TD)
2. Observador de Estado Extendido (ESO)
3. Ley de control no lineal (NLSEF)

La interacción entre estos componentes permite lograr estabilidad robusta frente a perturbaciones no modeladas[3].

### 2.2. Ecuaciones Fundamentales
El ESO se define mediante el siguiente sistema de ecuaciones:

$$
\begin{cases} 
\dot{z}_1 = z_2 + \beta_1 e \\ 
\dot{z}_2 = z_3 + b_0 u + \beta_2 e \\ 
\dot{z}_3 = \beta_3 e
\end{cases}
$$

Donde $$e = y - z_1$$ representa el error de estimación y $$\beta_i$$ son ganancias ajustables que determinan el desempeño del observador[1].

## 3. Implementación Práctica

### 3.1. Estrategia de Control
La señal de control $$u$$ se calcula mediante:

$$
u = \frac{u_0 - z_3}{b_0}
$$

Donde $$u_0$$ es una acción de control PD convencional y $$z_3$$ corresponde a la estimación de la perturbación total[1].

💡**Ejemplo 1:** En un sistema de levitación magnética, el ADRC compensa variaciones de carga del 30% manteniendo errores de posición inferiores a 10 µm, demostrando su eficacia en aplicaciones de alta precisión[3].

## 4. Análisis Comparativo

### 4.1. ADRC vs. Control PID
| **Parámetro**       | **ADRC**                                  | **PID**                     |
|----------------------|-------------------------------------------|-----------------------------|
| **Modelado**         | No requiere modelo preciso               | Necesita modelado exacto    |
| **Robustez**         | Alta contra perturbaciones               | Sensible a variaciones      |
| **Respuesta**        | Adaptativa no lineal                     | Lineal fija                 |
| **Complexidad**      | Implementación moderada                  | Simple implementación       |

Tabla 1. Comparación de características entre ADRC y PID

## 5. Casos de Estudio

### 5.1. Regulación de Nivel en Tanques
Para un tanque con área variable $$A(h)$$, el término no lineal $$\frac{a\sqrt{2gh}}{A(h)}$$ se trata como perturbación, permitiendo control preciso sin modelado geométrico explícito[1].

### 5.2. Control de Velocidad en Motores DC
Implementación en motores con fricción variable muestra tiempos de estabilización 3 veces menores que controladores PI convencionales (0.4s vs 1.2s)[3].

## 6. Conclusiones
El ADRC emerge como técnica potente para control robusto, destacando en:
- Manejo de no linealidades complejas
- Rechazo activo de perturbaciones
- Reducción de dependencia de modelos precisos

Limitaciones principales incluyen complejidad de sintonización y requerimiento de conocimiento especializado para implementación óptima.

## 8. Referencias
[1] Dialnet: ADRC Una Estrategia de Control Robusto  
[2] Archivos complementarios de implementación práctica
