# KineStep: Panel Generador de Energía Cinética ⚡

**Universidad Nacional de Colombia | Grupo: Materia Oscura**

KineStep es un proyecto de *Energy Harvesting* (recolección de energía) diseñado para transformar la energía cinética desperdiciada en las pisadas humanas en electricidad limpia y utilizable. Mediante un sistema de inducción electromagnética, demostramos cómo el movimiento cotidiano puede ser una fuente viable de energía a pequeña escala.

---

## 🚨 Planteamiento del Problema

En las sociedades modernas, la demanda energética y la necesidad de transicionar hacia fuentes de energía limpia han impulsado la búsqueda de métodos descentralizados de generación. En entornos urbanos de alta densidad, como los campus universitarios, se disipa continuamente una enorme cantidad de energía mecánica en forma de impactos contra el suelo debido al tránsito peatonal. 

El problema principal radica en la falta de sistemas eficientes y económicos de microgeneración capaces de capturar esta energía intermitente. Adicionalmente, la electricidad generada por impactos mecánicos irregulares es una **corriente alterna altamente inestable**, lo que impide su uso directo en dispositivos electrónicos (como diodos LED o sensores) sin provocar parpadeos o fallos continuos en el suministro.

---

## 🔬 Principios Físicos y Científicos

El núcleo de nuestro panel generador se basa en el principio de inducción electromagnética, gobernado principalmente por la **Ley de Faraday**. Esta ley establece que un campo magnético que cambia con el tiempo a través de un circuito de cable inducirá una fuerza electromotriz (FEM) o voltaje. 

La ecuación matemática que describe este fenómeno es:

$$\mathcal{E} = -N \frac{d\Phi}{dt}$$

Donde:
* **$\mathcal{E}$** es la fuerza electromotriz (voltaje) inducida.
* **$N$** es el número de espiras (vueltas) de la bobina.
* **$\frac{d\Phi}{dt}$** representa la tasa de cambio del flujo magnético ($\Phi$) a lo largo del tiempo. 
* El signo negativo obedece a la **Ley de Lenz**, indicando que la corriente inducida crea un campo magnético que se opone al cambio inicial que lo produjo.

En **KineStep**, el cambio de flujo magnético ($\frac{d\Phi}{dt}$) se logra mecánicamente: al pisar la baldosa, un sistema de resortes empuja rápidamente un imán permanente a través del centro hueco de nuestra bobina.

---

## 🛠️ Justificación de Materiales Seleccionados

Cada componente de KineStep fue elegido mediante un análisis cuidadoso para maximizar la eficiencia del circuito y garantizar su funcionamiento con el tipo específico de energía mecánica que produce una pisada (movimiento corto y de baja frecuencia).

### 1. Imán de Neodimio
* **Por qué:** Los imanes de neodimio son los imanes permanentes con mayor densidad de flujo magnético disponibles comercialmente. Dado que el desplazamiento mecánico de una pisada es corto (apenas unos centímetros), necesitamos un campo magnético extremadamente denso para generar una variación ($\frac{d\Phi}{dt}$) lo suficientemente grande como para inducir un voltaje útil. Un imán de ferrita común no produciría un pulso perceptible.

### 2. Alambre de Cobre Esmaltado (Calibre Fino)
* **Por qué:** Observando la Ley de Faraday, el voltaje es directamente proporcional a $N$ (número de espiras). Para alcanzar voltajes prácticos (superiores a 3V) en el pequeño volumen que ofrece la baldosa, necesitamos miles de vueltas. Un alambre de cobre de calibre muy fino permite enrollar un alto número de espiras en un carrete muy compacto, maximizando el voltaje de salida.

### 3. Diodos Schottky (1N5817) para Puente Rectificador
* **Por qué:** La bobina genera corriente alterna (AC), pero para almacenarla necesitamos corriente directa (DC). Usamos un puente rectificador de onda completa, pero elegimos específicamente **diodos Schottky** en lugar de diodos rectificadores comunes. Los diodos Schottky tienen una caída de tensión muy baja (aprox. 0.2V frente a los 0.7V estándar). En un sistema de microgeneración donde cada milivoltio cuenta, esta elección minimiza las pérdidas de energía en forma de calor durante la rectificación.

### 4. Condensador Electrolítico (470µF a 16V)
* **Por qué 16V:** Funciona como factor de seguridad. Un pisotón inusualmente fuerte puede generar picos de voltaje transitorios altos. Un límite de 16V evita que el condensador estalle o se degrade prematuramente.
* **Por qué 470µF:** Es el equilibrio ideal de capacitancia. Un valor muy bajo almacenaría muy poca energía para un trabajo útil, mientras que un valor muy alto requeriría demasiadas pisadas consecutivas para cargarse. 470µF permite acumular suficiente carga para un destello LED potente en solo un par de pisadas.

### 5. Diodo Zener (3.3V) y Transistor NPN
* **Por qué:** Este conjunto forma un circuito de disparo. Si conectáramos el LED directamente al condensador, la energía se drenaría de forma lenta e imperceptible a medida que se carga. El Diodo Zener actúa como una compuerta que solo se abre cuando el tanque alcanza exactamente 3.3V. Al llegar a este umbral, activa el transistor, el cual libera toda la energía acumulada de golpe hacia el LED, produciendo un flash brillante y notorio.

---

## 💻 Diseño Experimental y Simulación con Arduino

Para fines de demostración técnica y validación del circuito electrónico en presentaciones en vivo o videos, KineStep integra una etapa de simulación apoyada en un **Arduino**. 

Dado que el módulo electromecánico construido es un prototipo básico diseñado exclusivamente para validar el principio de Faraday físico, utilizar un Arduino nos permite simular la **corriente alterna continua** que generaría un modelo a escala industrial (con múltiples baldosas y tránsito constante). De esta manera, podemos demostrar el funcionamiento del circuito rectificador y de disparo con mayor estabilidad, claridad didáctica y facilidad, comprobando cómo se limpia la señal sin depender de pisadas constantes en la mesa de laboratorio.

---

## 📊 Resultados y Análisis de Datos

Durante las pruebas experimentales, se evaluó el comportamiento del voltaje en el condensador integrador y su impacto sobre la carga final (LED). A continuación, se presenta la tabla de recolección de energía utilizando la señal simulada de la pisada:

| Tiempo (s) | Voltaje Condensador (V) | Estado del LED |
| :---: | :---: | :--- |
| 0.0 | 0.00 | Apagado (Región de Corte) |
| 1.0 | 1.20 | Apagado (Cargando) |
| 2.0 | 2.50 | Apagado (Cargando) |
| 3.0 | 3.40 | Apagado (Umbral Zener alcanzado) |
| 3.5 | 4.02 | **Disparo / Destello Limpio (Saturación)** |
| 3.6 | 0.40 | Apagado (Reinicio de ciclo) |

**Análisis:**
El circuito resuelve con éxito el problema inicial del voltaje mecánico crudo. Al conectar un LED directo a la bobina, este experimentaba un "parpadeo" inestable. Con el circuito propuesto, el condensador acumula energía de forma limpia hasta que el diodo Zener permite la activación del transistor (cerca de los 4.0V), liberando un pulso de corriente robusto que garantiza un destello constante y definido.

---

## 🎯 Conclusiones

1. Se validó de forma experimental la **Ley de Faraday**, comprobando que un embobinado de alta densidad (cable fino) compensa mecánicas de corto desplazamiento para generar voltajes aprovechables en la recolección de microenergía.
2. El diseño del **circuito de acondicionamiento de señal** logró corregir exitosamente la inestabilidad inherente a la corriente electromecánica peatonal, convirtiendo picos erráticos en pulsos de luz limpios y potentes mediante almacenamiento capacitivo.
3. El uso de microcontroladores (Arduino) como **herramienta de simulación** resulta altamente eficaz para validar y calibrar circuitos en etapas tempranas de prototipado sin depender de estrés mecánico constante.

---

## 🚀 Limitaciones y Propuestas de Mejora

* **Limitaciones actuales:** El alambre ultrafino necesario para elevar el voltaje ($N$ alto) incrementa la resistencia interna de la bobina, causando pequeñas pérdidas por efecto Joule. Asimismo, el circuito de disparo pasivo (Zener) tiene un umbral rígido que no se ajusta dinámicamente según la carga.
* **Trabajo Futuro:** Implementar un circuito integrado especializado en *Energy Harvesting* (como un Boost Converter de ultra bajo consumo) para reemplazar la circuitería pasiva y aprovechar voltajes de entrada aún menores. Adicionalmente, el diseño mecánico podría beneficiarse de micro-engranajes para multiplicar la velocidad del imán al descender, incrementando significativamente $\frac{d\Phi}{dt}$.

---

## 👥 Equipo Integrante

* **Julián Mateus Lizarazo Duarte** - *Director Ejecutivo*
* **Juan Angel Vargas Rodríguez** - *Director Científico / Ingeniería Mecatrónica*
* **David Santiago Cuéllar López** - *Director Científico / Ingeniería Mecatrónica*
* **Santiago Galindo Hernandez** - *Director Creativo / Ingeniería Agrícola*
* **Juan Pablo Trujillo Delgadillo** - *Director Financiero*

---

## 📚 Referencias Bibliográficas

1. Serway, R. A., & Jewett, J. W. (2018). *Física para ciencias e ingeniería* (10a ed.). Cengage Learning. (Capítulo sobre Ley de Faraday e Inducción).
2. Boylestad, R. L., & Nashelsky, L. (2009). *Electrónica: Teoría de circuitos y dispositivos electrónicos* (10a ed.). Pearson Educación.
3. Priya, S., & Inman, D. J. (Eds.). (2009). *Energy Harvesting Technologies*. Springer Science & Business Media.
