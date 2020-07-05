---
weight: 1
bookFlatSection: false
title: "Plan Documentación"
---

# Plan de Documentación Finvivir

## **Propósito** 
Este documento contiene la propuesta del plan, contenido, y tiempos de entrega de la documentación para el proyecto Finvivir.

## **Público**
Desarrolladores y colaboradores del proyecto Finvivir. 

{{< rawhtml >}}
<br />
{{< /rawhtml >}}

## **Entregables**
Esta sección describe la documentación propuesta y describe la tabla de contenido de cada documento entregable. 

{{< rawhtml >}}
<table>
    <thead>
        <tr class="header">
            <th><strong>Tópico</strong></th>
            <th><strong>Descripción</strong></th>
            <th><strong>Documentos Propuestos</strong></th>
        </tr>
    </thead>
    <tbody>
        <tr class="odd">
            <td>Lógica Negocios Finvivir</td>
            <td>Incluye documentación relacionada y enfocada al entendimiento de la lógica de negocio de Finvivir.</td>
            <td>
                <ul>
                    <li>
                        <p>Glosario de términos</p>
                    </li>
                    <li>
                        <p>Reglas de negocio (TBD)</p>
                    </li>
                    <li>
                        <p>Diagrama de roles y usuarios</p>
                    </li>
                    <li>
                        <p>Historias de usuario</p>
                    </li>
                </ul>
            </td>
        </tr>
        <tr class="even">
            <td>Arquitectura</td>
            <td>Incluye documentación sobre las decisiones y los cambios derivados de éstas para crear una arquitectura
                limpia y funcional.<br />
                También provee una descripción detallada de la arquitectura final del proyecto a nivel sistema,
                componentes, así como de sus propiedades y relaciones.</td>
            <td>
                <ul>
                    <li>
                        <p>Esquema de decisiones y cambios de la Arquitectura (TBD)</p>
                    </li>
                    <li>
                        <p>Guía de Arquitectura</p>
                    </li>
                </ul>
            </td>
        </tr>
        <tr class="odd">
            <td>Microservicios</td>
            <td>Incluye documentación relacionada a cada uno de los microservicios del proyecto Finvivir: core,
                créditos, incidencias, beneficios, reportes y notificaciones.</td>
            <td>
                <ul>
                    <li>
                        <p>Guía de desarrollo del microservicio</p>
                        <ul>
                            <li>
                                <p>Resumen</p>
                            </li>
                            <li>
                                <p>Arquitectura</p>
                            </li>
                            <li>
                                <p>Diagramas entidad/relación</p>
                            </li>
                            <li>
                                <p>Endpoints (APIs) - Swagger</p>
                            </li>
                            <li>
                                <p>Dependencias</p>
                            </li>
                            <li>
                                <p>Runbooks</p>
                            </li>
                            <li>
                                <p>Casos de uso (TBD)</p>
                            </li>
                        </ul>
                    </li>
                    <li>
                        <p>Guía de onboarding frontend (README)</p>
                        <ul>
                            <li>
                                <p>Credenciales</p>
                            </li>
                            <li>
                                <p>Requerimientos</p>
                            </li>
                            <li>
                                <p>Prácticas de código</p>
                            </li>
                            <li>
                                <p>Repositorios</p>
                            </li>
                            <li>
                                <p>Establecimiento de ambientes de desarrollo, producción, y pruebas</p>
                            </li>
                            <li>
                                <p>Canales de comunicación</p>
                            </li>
                            <li>
                                <p>Contacto</p>
                            </li>
                        </ul>
                    </li>
                </ul>
            </td>
        </tr>
        <tr class="even">
            <td>Frontend</td>
            <td>Incluye documentación relacionada al desarrollo e integración del frontend</td>
            <td>
                <ul>
                    <li>
                        <p>Guía de desarrollo frontend</p>
                        <ul>
                            <li>
                                <p>Integración cognito</p>
                            </li>
                            <li>
                                <p>Componente clientes</p>
                            </li>
                            <li>
                                <p>Componente créditos</p>
                            </li>
                        </ul>
                    </li>
                    <li>
                        <p>Guía de onboarding frontend (README)</p>
                    </li>
                </ul>
            </td>
        </tr>
        <tr class="odd">
            <td>Estrategias</td>
            <td>Incluye la documentación de los planes y estrategias de diferentes áreas involucradas en el proyecto:
                Datos, DevOps, Documentación, y Pruebas y control de calidad.</td>
            <td>
                <ul>
                    <li>
                        <p>DataOps</p>
                    </li>
                    <li>
                        <p>DevOps</p>
                    </li>
                    <li>
                        <p>DocOps</p>
                    </li>
                    <li>
                        <p>QA</p>
                    </li>
                </ul>
            </td>
        </tr>
    </tbody>
</table>
{{< /rawhtml >}}

{{< rawhtml >}}
<br />
{{< /rawhtml >}}

## **Revisión y Aprobación**
La documentación de Finvivir requiere de la revisión y subsecuente aprobación de las siguientes personas:

|**Nombre**|**Descripción**|
|--- |--- |
|SME|Persona experta en el área de frontend, backend, data, devops, o QA (equipo Wizeline extendido)|
|Hassan Reyes|Líder técnico (Wizeline)|
|Hugo Morales|PjM (Wizeline)|
|Daniel Treviño|Propietario del producto (Finvivir)|

{{< rawhtml >}}
<br />
{{< /rawhtml >}}

## **Presunciones, Dependencias, y Riesgos**
Esta sección lista las presunciones, dependencias, y riesgos de la documentación relacionada al proyecto de Finvivir. 

### Presunciones
El escritor técnico asume lo siguiente:
- La documentación se genera, revisa, y aprueba mediante una participación activa del equipo de desarrollo. 
- La creación de una estrategia de DocOps (documentación automatizada) es una herramienta que puede agilizar el proceso de documentación si, y sólo si, el equipo de desarrollo se involucra en el proceso de documentación. 
- La documentación se entrega en un sitio estático gestionado por Gitlab.


### Dependencias
La documentación de Finvivir tiene las siguientes dependencias:
- Las estimaciones se basan en el objetivo actual del proyecto y cambiarán conforme al alcance del mismo.
- El personal del área de operaciones, contabilidad, tecnologías de información, y otras partes interesadas de Finvivir, debe participar en la generación, revisión, y aprobación de contenido para la documentación.
- Los miembros del equipo de desarrollo deben estar disponibles para revisar la documentación en sus respectivas áreas de experiencia.
- Las revisiones de la documentación deben completarse de acuerdo con el cronograma propuesto.

### Riesgos
La documentación de Finvivir tiene los siguientes riesgos:
- La falta de disponibilidad de ingenieros y otros revisores afectará la generación y revisión de la información.
- Las revisiones tardías e incompletas pueden evitar la creación de documentación de alta calidad.
- Los cambios tardíos en los procedimientos y requisitos pueden evitar la entrega oportuna de la documentación.
- La falta de consenso entre los equipos en relación al contenido y estilo de la documentación puede afectar negativamente su consistencia y, por lo tanto, la usabilidad de la documentación en conjunto.
