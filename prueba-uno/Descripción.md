## Enunciado
Prueba 1 - Diagrama de Red Produzca un diagrama de red (puede utilizar
lucidchart) de una aplicación web en GCP o AWS y escriba una descripción de
texto de 1/2 a 1 página de sus elecciones y arquitectura.
El diseño debe soportar:
• Cargas variables
• Contar con HA (alta disponibilidad)
• Frontend en Js
• Backend con una base de datos relacional y una no relacional
• La aplicación backend consume 2 microservicios externos
El diagrama debe hacer un mejor uso de las soluciones distribuidas.

## Resolución
Se eligió AWS como plataforma de desarrollo del sistema.

La arquitectura propuesta consta de los siguientes componentes y servicios distribuidos:
-Virtual Private Cloud: tener una red virtual aislada en la nube permite gestion total sobre configuracion e infraestructura de red en la nube. Como principales caracteristicas aporta aislamiento, control de direcciones IP, conectividad, controles de seguridad y flexibilidad y escalabilidad.
-Availability zones: se incluyeron en el diseño ya que cada una aporta disponibilidad de los recursos de una manera independiente (resiliencia y alta disponibilidad) permitiendo distribuir pedidos en diferentes zonas en casos de fallo. Aseguran baja latencia y permiten la distribución de cargas.
-Application load balancer: Se utiliza un balanceador de carga para distribuir el tráfico de la aplicación web de manera equilibrada entre las varias zonas de disponibilidad. Esto garantiza una alta disponibilidad (no es su principal causante) y la capacidad de manejar cargas variables.
-Public subnets: Al estar asociadas a una tabla de ruteo a una IGW permiten que las instancias de los servicios contenidos en ellas, tengan conectividad directa a internet.
-Private subnets: No tienen dir IP publica asociada por lo que no tienen salida directa a internet. En el caso de las instancias backend que deberian consumir servicios externos, se utilizan NAT gateways para traducir dirs de red y rutear el trafico hacia internet.
(Cabe destacar que el trafico entre subredes pub/priv se puede realizar sin problemas dentro de la VPC, si las politicas de seguridad lo permiten)
-Auto-scaling groups: Mediante reglas permiten ajustar el numero de instancias de EC2's de manera automatica segun la demanda que sea necesaria. Se incluyo este mecanismo en la arquitectura para asegurar alta disponibilidad y en combinacion con el ELB, el balanceo de cargas.
-EC2 instances: servidores virtuales que permiten escalabilidad horizontal y vertical.