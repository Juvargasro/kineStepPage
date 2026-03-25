# KineStep: Panel Generador de Energía Cinética ⚡

**Universidad Nacional de Colombia | Grupo: Materia Oscura**

KineStep es un proyecto de *Energy Harvesting* (recolección de energía) diseñado para transformar la energía cinética desperdiciada en las pisadas humanas en electricidad limpia y utilizable. Mediante un sistema de inducción electromagnética, demostramos cómo el movimiento cotidiano puede ser una fuente viable de energía a pequeña escala.

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
* **Por qué:** Observando la Ley de Faraday, el voltaje es directamente proporcional a $N$ (número de espiras). Para alcanzar voltajes prácticos (superiores a 3V) en el pequeño volumen que ofrece la baldosa, necesitamos miles de vueltas. Un alambre de cobre de calibre muy fino (ej. AWG 30 o 32) permite enrollar un alto número de espiras en un carrete muy compacto, maximizando el voltaje de salida.

### 3. Diodos Schottky (1N5817) para Puente Rectificador
* **Por qué:** La bobina genera corriente alterna (AC), pero para almacenarla necesitamos corriente directa (DC). Usamos un puente rectificador de onda completa, pero elegimos específicamente **diodos Schottky** en lugar de diodos rectificadores comunes (como el 1N4007). Los diodos Schottky tienen una caída de tensión muy baja (aprox. 0.2V frente a los 0.7V estándar). En un sistema de micro-generación donde cada milivoltio cuenta, esta elección minimiza las pérdidas de energía en forma de calor durante la rectificación.

### 4. Condensador Electrolítico (470µF a 16V)
* **Por qué 16V:** Funciona como factor de seguridad. Un pisotón inusualmente fuerte puede generar picos de voltaje transitorios altos. Un límite de 16V evita que el condensador estalle o se degrade prematuramente.
* **Por qué 470µF:** Es el equilibrio ideal de capacitancia. Un valor muy bajo (ej. 10µF) almacenaría muy poca energía para un trabajo útil, mientras que un valor muy alto (ej. 4700µF) requeriría demasiadas pisadas consecutivas para cargarse hasta el voltaje operativo. 470µF permite acumular suficiente carga para un destello LED potente en solo un par de pisadas.

### 5. Diodo Zener (3.3V) y Transistor NPN
* **Por qué:** Este conjunto forma un circuito de disparo. Si conectáramos el LED directamente al condensador, la energía se drenaría de forma lenta e imperceptible a medida que se carga. El Diodo Zener actúa como una compuerta que solo se abre cuando el tanque (condensador) alcanza exactamente 3.3V. Al llegar a este umbral, activa el transistor, el cual libera toda la energía acumulada de golpe hacia el LED, produciendo un flash brillante y notorio que demuestra visualmente el éxito de la generación.

---

## 👥 Equipo Integrante
* **Juan Diego Aldana Pérez** - *Director Ejecutivo*
* **Juan Angel Vargas Rodríguez** - *Director Científico / Ingeniería Mecatrónica*
* **David Santiago Cuéllar López** - *Director Científico / Ingeniería Mecatrónica*
* **Santiago Galindo Hernandez** - *Director Creativo / Ingeniería Agrícola*
* **Juan Pablo Trujillo Delgadillo** - *Director Financiero*
