# Lab 1 · Decisión

## 1. Tabla de resultados
| Configuración | Aciertos | Inválidas | Tokens | Segundos | Costo estimado (USD) |
|---|---|---|---|---|---|
| cascada-armada | 20/20 | 0 | 17003 | 110.8 | 0.0 |
| nube-chico | 20/20 | 0 | 14201 | 59.3 | 0.0 |
| nube-grande | 20/20 | 0 | 5914 | 114.8 | 0.0 |

## 2. Gráfico
(resultados/grafico.svg)
En aciertos ambos modelos acertaron pero en cantidad de tokens se observa el modelo de nube grande consumió menos tokens


## 3. Casos importantes
No hubo desacuerdos en los casos pero si se observa diferencia en el nivel de confianza el modelo de nube-chica tuvo más respuestas con confianza baja que el modelo de nube-grande 


## 4. Regla de ruteo de modelos

Se ejemplifica con tres tareas diferentes de clasificación de reclamos. 
| Tarea | Modelo / configuración | Por qué (dato medido) | Riesgo y privacidad | Cuándo escalar |
|---|---|---|---|---|
| Clasificar reclamos (lote) | nube-grande | 20/20 con 5.914 tokens, 2,4 veces menos que nube-chico | Los reclamos tienen datos personales y financieros enviados a terceros (OpenRouter y proveedor; los modelos gratuitos pueden registrar los prompts). Anonimizar nombres, tarjetas, cuentas y documentos, o usar un modelo local. | Confianza baja (R17, R20) o respuesta inválida: revisión humana |
| Clasificar reclamos (tiempo real) | nube-chico | 20/20 en 59.3 s, la mitad de latencia | Igual que arriba | Confianza baja: nube-grande. Si este también duda: revisión humana |
| sospecha_fraude (cualquier modo) | El que corresponda, más revisión humana | R17: los dos modelos dudaron | Un error tiene alto impacto (bloquear a un cliente o dejar pasar un fraude) | Siempre |

## 5. Lo que el chequeo no verifica

No se observó errores pero se escalo innecesariamente en las respuestas que daban confianza bajapero que si se acertó.