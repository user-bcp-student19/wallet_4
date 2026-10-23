# W1: Registro y habilitación de la wallet

Como usuario de smartphone que realiza transferencias diarias de bajo monto,
quiero completar el registro mediante un flujo guiado y entender el resultado de la verificación,
para activar mi wallet cuando cumpla los requisitos y poder acceder al flujo de pagos.

## Alcance

- W1 cubre el registro, la validación de datos, la consulta del resultado KYC y la habilitación de la wallet.
- El acceso a pagos se habilita únicamente cuando la wallet está `ACTIVE`. La ejecución y confirmación de pagos pertenecen a W2.
- Para el prototipo MVP, KYC se representa mediante el mock y datos sintéticos; no se realiza verificación real ni movimiento de dinero.

## Criterios de aceptación

1. Durante el onboarding, el usuario puede identificar los pasos requeridos, el paso actual y su progreso.
2. Si falta un dato obligatorio o tiene un formato inválido, el usuario no puede avanzar. El campo correspondiente muestra cómo corregirlo y los demás datos válidos se conservan.
3. Cuando la verificación resulta aprobada, la wallet queda en estado `ACTIVE` y el usuario puede acceder al punto de entrada de pagos.
4. Cuando la verificación queda pendiente de revisión, la wallet no se activa ni permite acceder a pagos. El usuario ve que la revisión está pendiente y el siguiente paso disponible.
5. Cuando la verificación es rechazada, la wallet no se activa ni permite acceder a pagos. El usuario recibe un mensaje claro sobre el resultado y la acción disponible según la política definida por Producto y Cumplimiento.
6. Si el servicio de verificación no está disponible, la wallet no se presenta como activa y el usuario recibe un mensaje que le permite entender que puede reintentar.
7. El flujo emite eventos de inicio, finalización de paso y resultado del onboarding. El evento de onboarding completado solo se emite cuando la wallet queda `ACTIVE`; los eventos no incluyen documentos ni otros datos KYC.

## Contexto

- Épica: [MVP de wallet en Perú](userstories/packages/epic/peru-wallet-mvp.sp.md).
- La épica establece como objetivo reducir la mediana de finalización del onboarding de 8 a 3 minutos. Esta es una métrica de resultado del producto, no una condición que pueda garantizar por sí sola esta historia.
- La historia de [confirmación de pagos de bajo monto](userstories/packages/user-stories/payer-low-value-payment-confirmation.sp.md) define la transacción exitosa como evento de activación para el cálculo de MAU. Completar onboarding activa la wallet, pero no convierte por sí solo al usuario en activo mensual.
- El flujo KYC contempla resultados aprobados, pendientes y rechazados, además de indisponibilidad del servicio.

## Fuera de alcance

- Definir las reglas regulatorias, los documentos requeridos o las decisiones de elegibilidad KYC.
- Implementar KYC real, integraciones bancarias o movimiento de fondos.
- Ejecutar pagos y mostrar su resultado final; corresponde a W2.
- Generar reportes de MAU, atribuir gasto de adquisición o calcular CAC. Son necesidades de analítica de producto y negocio, no del flujo W1.

## Supuestos y dependencias

- Producto y Cumplimiento definirán los campos obligatorios, las reglas KYC y las acciones permitidas ante un rechazo o una revisión pendiente.
- El prototipo usa KYC simulado, identificadores y datos sintéticos; sus resultados no representan una decisión regulatoria real.
- El objetivo de MAU de 1,000 a 2,000 y el CAC de PEN 10 son objetivos de negocio definidos por el Product Owner en la épica.

## Preguntas abiertas

- ¿Qué pasos y campos obligatorios quedan aprobados por Producto y Cumplimiento para W1?
- ¿Qué acción concreta puede realizar el usuario mientras la verificación está pendiente o después de un rechazo?
- ¿Dónde se persisten los eventos analíticos y cómo se distingue una salida explícita de una sesión interrumpida?
- ¿Qué regla de inicio, finalización y pausa se usará para calcular la mediana de tiempo de onboarding?
