# Notificación

Cuando una transacción es procesada, una notificación HTTP (Webhook) es enviada al comercio.

Para recibir notificaciones se debe enviar el campo `notificationURL` con una URL de notificación. Cada vez que una transacción se procese se hará una petición HTTP a ese endpoint con información útil sobre el estado de la transacción.

```json
{
  "status": {
    "status": "APPROVED",
    "reason": "00",
    "message": "Aprobada",
    "date": "2024-07-11T15:22:37-05:00"
  },
  "internalReference": 1,
  "reference": "5834381",
  "signature": "9c0f8ff164d0af4a795f71ee127d8926f56d05fb"
}
```

## Recepción de Notificación

Para aprovechar esta notificación, en tu aplicación debes:

**Identificar la transacción:** Con el `internalReference` y `reference` debes buscar el pago en tu sistema, este debe coincidir con una transacción que hayas creado anteriormente.

**Validar firma del mensaje:** Se puede validar que la notificación se trate de un mensaje confiable de Placetopay generando y comparando el `signature`.

El signature se genera con la siguiente fórmula: `SHA-1(internalReference + status.status + secretKey)`

Si el `signature` generado es igual al `signature` que llegó en el mensaje, entonces la notificación es auténtica.

**Actualizar Información:** Si todo lo que necesitas es el estado final de la transacción, entonces puedes actualizar el estado en tu sistema y eso sería todo.

Si necesitas conocer información adicional, debes consultar la transacción usando el `internalReference`