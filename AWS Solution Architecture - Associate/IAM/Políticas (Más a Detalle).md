**Las políticas de IAM son la base de una sólida seguridad de IAM. Entender cómo funcionan las políticas y poder interpretarlas es fundamental para el éxito como Arquitecto y en el examen**

https://docs.aws.amazon.com/es_es/IAM/latest/UserGuide/reference_policies_evaluation-logic.html

## Políticas de Identidad
Las políticas de identidad son políticas de IAM que se aplican a las identidades. Esto puede incluir tanto usuarios como roles  que los usuarios pueden asumir. Estas son diferentes a las políticas de recursos.

La respuesta predeterminada a todas las solicitudes es de Denegación implícita. Esta 'postura' puede ser anulada al permitir el acceso del usuario con una política de permisos, esto le otorga acceso al usuario porque ha sido explícitamente Permitido. El mismo proceso se puede hacer con un política de Denegar explícita. Esto denegará el acceso independiente de los permisos que pueda tener el usuario.

Ejemplo:
```json
{
	"Version": "2012-10-17",
	"Statement": [
		{
			"Sid": "ExplicitDenyIfNotTheOwner",
			"Effect": "Deny",
			"Action": [
				"datapipeline:ActivatePipeline",
				"datapipeline:AddTags",
				"datapipeline:DeactivatePipeline",
				"datapipeline:DeletePipeline",
				"datapipeline:DescribeObjects",
				"datapipeline:EvaluateExpression",
				"datapipeline:GetPipelineDefinition",
				"datapipeline:PollForTask",
				"datapipeline:PutPipelineDefinition",
				"datapipeline:Query0bjects",
				"datapipeline:RemoveTags",
				"datapipeline:ReportTaskProgress",
				"datapipeline:ReportTaskRunnerHeartbeat",
				"datapipeline:SetStatus",
				"datapipeline:SetTaskStatus",
				"datapipeline:ValidatePipelineDefinition"
			],
			"Resource": ["*"],
			"Condition": {
				"StringNotEquals": {"datapipeline:PipelineCreator": "${aws:userid}"}
			}
		}
	]
}
```

## Políticas de recursos
**Las políticas basadas en recursos se adjuntan a un recurso.**

A diferencia de una política basada en la identidad, una política basada en recursos especifica QUIÉN (qué principal) puede acceder a ese recurso. Los principales identificados dentro de una política basada en recursos incluyen cuentas, usuarios de IAM, usuarios federados, roles de IAM, sesiones de roles asumidos o servicios de AWS.
Ejemplo:
```json
{
	"Version": "2012-10-17",
	"Statment": [
		{
			"Effect": "Allow",
			"Principal":{
				"AWS": "arn:aws:iam::123456789012:user/carlossalazar"
			},
			"Action":"s3:*",
			"Resource": [
				"arn:aws:s3:::carlossalazar/*",
				"arn:aws:s3:::carlossalazar"
			]
		}
	]
}
```

# Diagrama de flujo

![[Pasted image 20260223092413.png]]

## Otro Ejemplo

```json
{
	"Version": "2012-10-17",
	"Statement": [
		{
			"Sid": "EnableDisableHongKong",
			"Effect": "Allow",
			"Action": [
				"account:EnableRegion",
				"account:DisableRegion"
			],
			"Resource": "*"
			"Condition": {
				"StringEquals": {"account: TargetRegion": "ap-east-1"}
			}
	
		},
		{
			"Sid": "ViewConsole",
			"Effect": "Allow",
			"Action": [
				"aws-portal:ViewAccount",
				"account: ListRegions"
			],
			"Resource": "*"
		}
	]
}
```

# Amazon Resource Names (ARN)
**Una forma de identificar de forma única los recursos de AWS**

Requerimos un ARN cuando se necesita especificar un recurso sin ambigüedades en todo AWS, como en las políticas de IAM, las etiquetas de Amazon Relational Database Servise (Amazon RDS) y las llamadas a API.

## Formato ARN

Los formatos específicos dependen del recurso. Para usar un ARN, reemplace el texto en cursiva por la información específica del recurso.

Tenga en cuenta que los ARN de algunos recursos omiten la Región, el ID de cuenta o tanto la Región como el ID de cuenta.
```arn
	arn:partition:service:region:account-id:resource-id
	arn:partition:service:region:account-id:resource-type/resource-id
	arn:partition:service:region:account-id:resource-type:resource-id
```

# La importancia de los roles de IAM
**Los roles son una forma para que los usuarios obtengan permisos temporalmente**

Los roles de AWS tienen la misma composición que un usuario de IAM con las siguientes diferencias:
- Un rol de IAM no tiene credenciales a largo plazo asociada. Un principal (usuario, máquina o identidad autenticada) asume el rol y hereda los permisos asignados al usuario.
- El acceso temporal se otorga mediante tokens (STS). La caducidad del token reduce los riesgos asociados con la fuga de credenciales o la reutilización.
- Un rol de IAM tiene una política de confianza que define qué condiciones deben cumplirse para permitir que otros principal lo asuman.

En general, hay cuatro escenarios en los que podrían usarse roles de IAM:
- Un servicio de AWS accede a otro servicio de AWS.
- Una cuenta de AWS accede a otra cuenta de AWS.
- Una identidad web de terceros necesita acceso (es decir, Google, Facebook, Cognito).
- Autenticación mediante federación SAML2.0 (SSO).

# Servicio de Token de Seguridad (STS)
**Solicitar credenciales temporales de privilegios limitados para AWS IAM**

## Tus usuarios O usuarios federados

STS permite proporcionar credenciales temporales de privilegios limitados para sus usuarios de IAM o usuarios que federe como parte de la autenticación de acceso. STS es un servicio que está disponible a nivel mundial.

## Generación de Credenciales

Las credenciales temporales pueden ser asumidas por identidades autorizadas a través del comando `sts:Assumerole*`. El proceso de autorización sigue el siguiente flujo:
![[Pasted image 20260223121817.png]]

### Revocación de Credenciales Temporales
**Los roles pueden ser asumidos por MUCHAS identidades que obtendrán todos los mismos permisos. ¿Qué pasa si esas credenciales se ven comprometidas?**

#### Políticas de confianza
Las políticas de confianza cambiantes solo afectan a las identidades que aún no han asumido el papel. Estos cambios de política **NO tienen impacto** en las credenciales existentes.

#### Políticas de Permiso
Cambiar la política de **PERMISOS** impactará **TODAS** las credenciales. Actualización de la política con una denegación en línea de **AWSRevokeOlderSessions** para cualquier sesión anterior a la actualidad. Esto cierra todas las identidades que actualmente han asumido el papel y aplica las nuevas políticas.