!define RECTANGLE class
!define INTERFACE interface
!define SYSTEMS_NODE component
!define ARROW_LEFT -[#000000]->

RECTANGLE SistemaDeReservas {
  + RealizarReserva()
  + CancelarReserva()
  + ConsultarDisponibilidad()
}

RECTANGLE SistemaDeFacturacion {
  + GenerarFactura()
  + ProcesarPago()
  + RegistrarVenta()
}

RECTANGLE SistemaDeSeguridad {
  + MonitorearCámaras()
  + RegistrarAccesos()
  + ActivarAlarma()
}

RECTANGLE SistemaDeInventario {
  + RegistrarEntrada()
  + RegistrarSalida()
  + ConsultarInventario()
}

SYSTEMS_NODE "Cibercafé" {
  RECTANGLE Cliente
  INTERFACE Usuario
  RECTANGLE Cajero
  RECTANGLE CajaRegistradora
  RECTANGLE CamarasSeguridad
  RECTANGLE Alarma
  SYSTEMS_NODE "Sistemas Internos" {
    SistemaDeReservas
    SistemaDeFacturacion
    SistemaDeSeguridad
    SistemaDeInventario
  }
}

Cliente --> Usuario
Cajero -[#000000]-> CajaRegistradora
CamarasSeguridad -[#000000]-> SistemaDeSeguridad
Alarma -[#000000]-> SistemaDeSeguridad
SistemaDeReservas --> SistemaDeFacturacion : Realizar Reserva
SistemaDeReservas --> SistemaDeReservas : Cancelar Reserva
SistemaDeReservas --> SistemaDeInventario : Registrar Reserva
SistemaDeFacturacion --> SistemaDeInventario : Registrar Venta
SistemaDeSeguridad --> SistemaDeSeguridad : Registrar Acceso
SistemaDeSeguridad --> Alarma : Activar Alarma
SistemaDeInventario --> SistemaDeInventario : Actualizar Inventario
