
# Estructura de las atestaciones

Tomando como referencia la implementación de las *attestations* o *credentials* de la implementación original de [Uport](https://whitepaper.uport.me), definiremos un *attestation* como una estructura JSON que contiene diferentes atributos y que incluye los valores validados.

	[ 
		{
			“header” : {
				"alg": "RS256",
				"typ": "JWT"
			}
			“payload” : {
				iss: <uPortId of issuer>,
				sub: <uPortId of subject>,
				iat: 1479850830,
				exp: 1511305200,
				loa: 3,
				claim: {
					“name” : “Juan García”
				}
				}
			“Signature” : {
				<JWT signature data>
			}
		}, 
		…
	]

Los atributos de cada atestación serán:

* `header`. Incluye información relativa a los algoritmos y al formato de entrega de la atestación
* `payload`. La información en sí misma que es validada. Se trata de un diccionario de clave valor:
  * `iss`, `<AlastriaId_del_emisor>`.
  * `sub`, `<AlastriaId_del_suejto>`.
  * `iat` y `exp`, como timestamps que acotan el período de validez del dato en sí mismo.
  * `loa`, como nivel de confianza o *level of assurance* sobre los datos. Se corresponderá con un valor en la escala eIDAS donde 3 es alto, 2 es sustancial y 1 es bajo. El valor 0 se corresponderá con datos autoalegados por el usuario.
 * `signature`, como los datos correspondientes a la firma de la información del `payload`.

Cada atestación, puede ser incluida en una lista de atestaciones, cada una firmada por separado. Hacerlo por separado en una lista o array incluyendo la firma individual de cada atestación por separado, permitirá al usuario tomar la decisión sobre qué uso dar a cada una de ellas sin revelar información del resto de parámetros que pudieran ser verificados como parte del mismo proceso.
