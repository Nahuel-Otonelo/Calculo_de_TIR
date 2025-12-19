# Monitor de TIR Real - Bonos CER (Argentina) 📈

Este proyecto permite calcular la **Tasa Interna de Retorno (TIR) Real** de por ahora los bonos ajustables por CER TX26 y TX28 (algún día el TX31) del mercado argentino. El script no está hardcodeado y la obtención del precio del bono y del CER del día actual, se obtiene automáticamente (al momento de correrse, queda actualizado al instante).

## 🚀 Características

* **Scraping de Precios en Tiempo Real**: Obtiene las cotizaciones "Dirty Price" directamente desde la página de IOL.
* **Conexión con API BCRA**: Obtiene el último valor del coeficiente CER mediante la API oficial del Banco Central de la República Argentina.
* **Cálculo de Flujos Dinámico**: Una clase `BonoCER` reconstruye el cronograma de pagos (interés y amortización), descontando automáticamente los cupones ya cobrados a la fecha.
* **TIR Real**: Calcula el rendimiento por encima de la inflación utilizando el método de Newton-Raphson para encontrar la raíz del Valor Presente Neto (VPN).

## 🛠️ Estructura del Proyecto

El código se organiza bajo el paradigma de **Programación Orientada a Objetos (POO)**:

1. **`obtener_tabla(url)`**: Se encarga del Web Scraping y la normalización de los datos de cotización.
2. **`obtener_ultimo_cer()`**: Gestiona la conexión con el BCRA, incluyendo una lógica de ordenamiento por fecha para asegurar la robustez del dato más reciente.
3. **Clase BonoCER**:
* `obtener_flujos()`: Calcula el capital residual y los flujos futuros según las condiciones de emisión.
* `calcular_tir()`: Realiza el ajuste deflactado del precio y ejecuta el motor de cálculo financiero.



## 📦 Instalación y Requisitos

Para ejecutar este Notebook, necesitarás las siguientes librerías de Python:

```bash
pip install pandas numpy requests scipy html5lib

```

## 📊 Ejemplo de Salida

Al ejecutar el monitor, obtendrás un reporte consolidado como el siguiente:

```text
Valor del CER Hoy: 670.3668

Bono: TX26 | Precio: $1167.00
  > Residual: 40.00% | TIR Real: 5.49%
----------------------------------------
Bono: TX28 | Precio: $1665.00
  > Residual: 60.00% | TIR Real: 6.97%
----------------------------------------

```

## ⚠️ Notas de Seguridad

El script utiliza `urllib3.disable_warnings()` para facilitar la conexión con los servidores del BCRA, los cuales a veces presentan certificados SSL no reconocidos por las librerías estándar. Se recomienda su uso para fines de análisis personal.


## 🤝 Feedback y Contribuciones (¡Se buscan errores!)

No soy del palo de las finanzas. Por eso, si encontrás un error en el cálculo, una inconsistencia en las condiciones de emisión de algún bono, o simplemente creés que el código podría ser más eficiente (¡seguro que sí!), por favor no dudes en decírmelo.

¿Cómo podés ayudar?

Abrí un Issue: Si encontrás algo que no funciona o un resultado que no te cuadra.

Pull Requests: Si querés proponer una mejora directa en el código.

Críticas constructivas: ¡Son más que bienvenidas! Todo feedback me ayuda a seguir creciendo como desarrollador.


## ⚠️ Descargo de Responsabilidad (Disclaimer)

Este proyecto ha sido desarrollado con fines puramente didácticos.

**No soy analista financiero**, no poseo formación académica formal en finanzas ni cuento con certificaciones de idoneidad ante organismos reguladores.

El código fue construido basándose exclusivamente en la lectura de las Condiciones de Emisión de los bonos y aplicando la definiciones matemáticas simples.

Sin Garantías: Los resultados no contemplan comisiones de brokers, impuestos (Bienes Personales/Ganancias) o desfases temporales.

No es Asesoramiento: El uso de este script no constituye una recomendación de compra o venta de activos financieros. Cada usuario es responsable de sus propias decisiones de inversión.

