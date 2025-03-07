# Diagrama-Cajeros

## Código
@startuml
state StandBy
state TarjetaIntroducida
state TarjetaNoValida
state IntroducirPIN
state ValidacionFallida
state ValidacionExitosa
state SeleccionTransaccion
state EjecutandoTransaccion
state FinalizarSesion
state TarjetaRetenida

[*] --> StandBy

StandBy --> TarjetaIntroducida : Introducir tarjeta
TarjetaIntroducida --> TarjetaNoValida : Tarjeta no válida
TarjetaNoValida --> StandBy : Expulsar tarjeta

TarjetaIntroducida --> IntroducirPIN : Tarjeta válida
IntroducirPIN --> ValidacionFallida : PIN incorrecto
ValidacionFallida --> IntroducirPIN : Reintentar (Máx. 3 intentos)
ValidacionFallida --> TarjetaRetenida : 3 intentos fallidos
TarjetaRetenida --> FinalizarSesion : Fin del proceso

IntroducirPIN --> ValidacionExitosa : PIN correcto
ValidacionExitosa --> SeleccionTransaccion : Ofrecer transacciones

SeleccionTransaccion --> EjecutandoTransaccion : Elegir transacción
EjecutandoTransaccion --> SeleccionTransaccion : Finalizar transacción
SeleccionTransaccion --> FinalizarSesion : Cancelar interacción

FinalizarSesion --> StandBy : Expulsar tarjeta
@enduml
