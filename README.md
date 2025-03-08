# C3C Francisco Mendez 091-14-9796
Timing Analysis sobre la FSM  (Caja Fuerte)
# Desarrollo

## Caja Fuerte

Ahora se procederá a realizar un contador el cual servirá para poder abrir una caja fuerte. Nuestro contador tendrá 2 botones, A y B, los cuales nos ayudarán a abrir nuestra caja con la combinación `A A B`. Si en el transcurso de la combinación se llegara a introducir mal algún botón, esta automáticamente regresará al estado inicial.

---

## Tabla de estados corregida

| Estado Actual | Entrada (A, B) | Estado Siguiente | Salida |
|--------------|---------------|-----------------|--------|
| `S0 (00)`   | `A = 1, B = 0` | `S1 (01)`      | `0`    |
| `S0 (00)`   | `A = 0, B = 1` | `S0 (00)`      | `0`    |
| `S1 (01)`   | `A = 1, B = 0` | `S2 (10)`      | `0`    |
| `S1 (01)`   | `A = 0, B = 1` | `S0 (00)`      | `0`    |
| `S2 (10)`   | `A = 1, B = 0` | `S2 (10)`      | `0`    |
| `S2 (10)`   | `A = 0, B = 1` | `S3 (11)`      | `1` (Abre caja) |
| `S3 (11)`   | `A = X, B = X` | `S0 (00)`      | `0`    |

---

## Análisis de Tiempo (Timing Analysis)

Para evaluar el rendimiento de la FSM, realizamos el análisis de tiempo considerando las compuertas lógicas y los flip-flops utilizados.

### Cálculo de la Frecuencia Máxima de Operación

La frecuencia máxima de operación se define como:

\[ f_{max} = \frac{1}{T_{clk}} \]

Donde:
- \( T_{clk} \) es el tiempo de propagación total del circuito.

El retardo total del circuito se obtiene sumando:
- Retardo de la lógica combinacional (compuertas lógicas entre flip-flops).
- Retardo de establecimiento (setup time) del flip-flop.

Si los retardos de las compuertas son \( t_{logic} \) y el setup time es \( t_{setup} \), la ecuación es:

\[ T_{clk} = t_{logic} + t_{setup} \]

Finalmente:

\[ f_{max} = \frac{1}{t_{logic} + t_{setup}} \]

### Cumplimiento de Restricción Hold

Para que el circuito funcione correctamente, debe cumplir la restricción de hold, es decir:

\[ t_{hold} \leq t_{clk\_to\_q} + t_{logic} \]

Donde:
- \( t_{hold} \) es el tiempo de retención del flip-flop.
- \( t_{clk\_to\_q} \) es el retardo del flip-flop al cambiar la salida.
- \( t_{logic} \) es el retardo de la lógica combinacional entre flip-flops.

Si esta condición no se cumple, la FSM podría producir estados incorrectos.

---
# Análisis de Prefijos Binarios y Almacenamiento

## Cálculos de Capacidad

Dado que el último dígito de mi carnet termina en **6**, se suman 5 unidades para obtener una capacidad hipotética de:

\[
6 + 5 = 11 \, 	ext{GB}
\]

### Conversión de 11 GB a GiB, KiB y TiB:

1. **GB a GiB:**
   Sabemos que 1 GiB = 1,073,741,824 bytes y 1 GB = 1,000,000,000 bytes, por lo que:

\[
	ext{Capacidad en GiB} = rac{11 \, 	ext{GB} 	imes 1,000,000,000 \, 	ext{bytes}}{1,073,741,824 \, 	ext{bytes por GiB}} = 10.22 \, 	ext{GiB}
\]

2. **GB a KiB:**
   Sabemos que 1 KiB = 1,024 bytes y 1 GB = 1,000,000,000 bytes:

\[
	ext{Capacidad en KiB} = 11 \, 	ext{GB} 	imes 1,000,000,000 \, 	ext{bytes} \div 1,024 \, 	ext{bytes por KiB} = 10,742,187.5 \, 	ext{KiB}
\]

3. **GB a TiB:**
   Sabemos que 1 TiB = 1,099,511,627,776 bytes y 1 GB = 1,000,000,000 bytes:

\[
	ext{Capacidad en TiB} = rac{11 \, 	ext{GB} 	imes 1,000,000,000 \, 	ext{bytes}}{1,099,511,627,776 \, 	ext{bytes por TiB}} = 0.010 \, 	ext{TiB}
\]

### Resumen de las conversiones:
- **11 GB** = **10.22 GiB**
- **11 GB** = **10,742,187.5 KiB**
- **11 GB** = **0.010 TiB**

---

## Respuesta a la Segunda Pregunta

Si el fabricante indica que tenemos **11 GB**, pero la conversión real es a **10.22 GiB**, vamos a calcular el porcentaje de "almacenamiento falso":

1. La diferencia entre **11 GB** y **10.22 GiB** en términos de GB:

\[
	ext{Diferencia} = 11 - 10.22 = 0.78 \, 	ext{GB "falsos"}
\]

2. El porcentaje de almacenamiento "mentira":

\[
	ext{Porcentaje de almacenamiento "mentira"} = \left( rac{0.78}{11} 
ight) 	imes 100  pprox 7.09\%
\]

**Porcentaje de almacenamiento "mentira" ofrecido por el fabricante: aproximadamente un 7.09%.**



## Conclusión

El diseño de la máquina de estados finitos (FSM) para la caja fuerte garantiza que la secuencia de entrada correcta (`A A B`) desbloquee la caja, mientras que cualquier error reinicia el sistema al estado inicial. Este método proporciona una forma segura y confiable de implementar un mecanismo de acceso controlado. Además, el uso de una FSM permite una implementación eficiente con circuitos digitales en Logisim Evolution o en hardware real.

Con el análisis de tiempo, se garantiza que el circuito funcione a una frecuencia adecuada sin violar restricciones de hold ni provocar errores en la transición de estados.

