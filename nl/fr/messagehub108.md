---

copyright:
  years: 2015, 2018
lastupdated: "2018-07-05"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Foire aux questions {{site.data.keyword.messagehub}}
{: #faqs}

Vous trouverez ici les réponses aux questions courantes concernant le service {{site.data.keyword.IBM}} {{site.data.keyword.messagehub}}.

<!--17/10/17 - Karen: same info duplicated at messagehub104 -->
## Comment utiliser des API Kafka pour créer et supprimer des sujets ?
{: #topic_admin}

Si vous utilisez la version 0.11 ou une version ultérieure du client Kafka, ou la version 0.10.2.0 ou une version ultérieure de Kafka Streams, vous pouvez employer des API pour créer et supprimer des sujets. Certaines restrictions s'appliquent aux paramètres autorisés lors de la création des sujets. Actuellement, vous ne pouvez modifier que les paramètres suivants :

<dl>
<dt>cleanup.policy</dt>
<dd>Défini sur <code>delete</code> (par défaut), <code>compact</code> ou <code>delete,compact</code>
<p>**Remarque :**
Si la règle de nettoyage est uniquement <code>compact</code>, <code>delete</code> est automatiquement ajouté, mais la suppression est désactivée selon l'heure. Les messages du sujet sont compactés jusqu'à 1 Go avant d'être supprimés.</p>
</dd>

<dt>retention.ms</dt>
<dd>La durée de conservation par défaut est de 24 heures. La durée minimale est d'une heure et la durée maximale de 30 jours. Spécifiez cette valeur comme un nombre d'heures.

<p>**Remarque :**
Dans le plan Enterprise, ce paramètre accepte toute valeur.</p>
</dd>

<dt>retention.bytes</dt>
<dd>Taille maximale que peut atteindre une partition (constituée de segments de journaux) avant suppression des anciens segments de journaux afin de libérer de l'espace.

<p>**Remarque :**
Plan Enterprise uniquement. Toute valeur supérieure à 1 Mo.</p>
</dd>

<dt>segment.bytes</dt>
<dd>Taille du fichier de segments du journal.

<p>**Remarque :**
Plan Enterprise uniquement. Toute valeur supérieure à 100 Mo.</p>
</dd>

<dt>segment.index.bytes</dt>
<dd>La taille de l'index qui met en correspondance des décalages et des positions de fichier. 

<p>**Remarque :**
Plan Enterprise uniquement. Toute valeur comprise entre 100 Ko et 2 Go.</p>
</dd>

<dt>segment.ms</dt>
<dd>La période de temps après laquelle Kafka force le journal reprendre l'enregistrement par écrasement des segments les plus anciens même si le fichier de segments n'est pas plein. 

<p>**Remarque :**
Plan Enterprise uniquement. Toute valeur comprise entre 5 minutes et 30 jours.</p>
</dd>
</dl>


## Quelle est la durée que {{site.data.keyword.messagehub}} définit dans la fenêtre de conservation des journaux pour le sujet Décalages consommateur ?
{: #offsets }
{{site.data.keyword.messagehub}} conserve les décalages consommateur pendant 7 jours. Cela correspond à la configuration Kafka offsets.retention.minutes. 

La conservation des décalages s'effectue au niveau du système. Vous ne pouvez donc pas la définir au niveau d'un sujet spécifique. Les groupes de consommateurs n'obtiennent que 7 jours de décalages stockés, même en utilisant un sujet dont la durée de conservation a été augmentée jusqu'au maximum de 30 jours. 

## Quel est le comportement en disponibilité de {{site.data.keyword.messagehub}} ?
{: #availability}

Si vous écrivez des applications {{site.data.keyword.messagehub}}, ces informations vous expliquent le comportement normal en disponibilité de {{site.data.keyword.messagehub}} et ce que vos applications sont censées traiter.

### API
{: #api_availability }

Dans le cadre du fonctionnement normal de {{site.data.keyword.messagehub}}, les noeuds des clusters Kafka sont parfois redémarrés.
Dans certains cas, vos applications sont conscientes de la réaffectation des ressources par le cluster. Ecrivez vos applications de telle sorte qu'elles soient résilientes face à ces changements et qu'elles puissent se reconnecter et reprendre leur fonctionnement.

### Ponts {{site.data.keyword.messagehub}} (plan Standard uniquement)
{: #bridge_availability }

Ecrivez vos applications de telle sorte qu'elles gèrent la possibilité d'un redémarrage occasionnel des ponts.

## Quelle est la taille de message maximale de {{site.data.keyword.messagehub}} ? 
{: #max_message_size }

La taille de message maximale de {{site.data.keyword.messagehub}} est 1 Mo, qui est la valeur par défaut Kafka. 

## Quels sont les paramètres de réplication de {{site.data.keyword.messagehub}} ? 
{: #replication }

{{site.data.keyword.messagehub}} est configuré de manière à offrir une forte disponibilité et durabilité.
Les paramètres de configuration suivants s'appliquent à tous les sujets et ne sont pas modifiables :
* replication.factor = 3
* min.insync.replicas = 2

## Comment fonctionne la facturation de {{site.data.keyword.messagehub}} sur le plan Standard ? 
{: #billing }

Sur le plan Standard, {{site.data.keyword.messagehub}} prélève régulièrement un décompte de sujets des utilisateurs et {{site.data.keyword.Bluemix_notm}} enregistre la valeur de prélèvement maximale chaque jour. {{site.data.keyword.messagehub}} facture en fonction de cette valeur maximale de partitions concurrentes visualisées et du nombre total de messages envoyés et reçus quotidiennement.

Par exemple, si vous créez et supprimez 1 sujet 10 fois au cours d'une journée, 1 sujet maximum vous sera facturé. En revanche, si vous créez 10 sujets puis les supprimez, vous pouvez être facturé de 0 ou de 10 sujets selon le moment où s'effectue le prélèvement.

{{site.data.keyword.messagehub}} facture chaque message ou tous les 64 k. Un message qui atteint 64 k compte comme 1 message facturable. Les messages de plus de 64 k correspondent à un nombre de messages facturables déterminé selon la formule suivante : <code><var class="keyword varname">taille_message</var> &divide; 64 k</code>.

<!--12/04/18 - Karen: same info duplicated at messagehub057 -->
## Quelle est la fréquence de redémarrage de l'API REST Kafka ? 
{: #REST_restart }

L'API REST Kafka redémarre une fois par jour pendant un court laps de
temps. 

Au cours de cette période, elle est susceptible de ne plus être disponible. Si cela se produit, il est conseillé de relancer votre demande. Après le redémarrage
de l'API REST, vous devez créer à nouveau vos instances consommateur Kafka. Dans ce cas,
l'API REST renvoie le code JSON suivant :

```'{"error_code":40403,"message":"Consumer instance not found."}'
```
{:screen}







