---

copyright:
  years: 2015, 2018
lastupdated: "2018-07-13"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Introduzione a Message Hub 
{: #messagehub}

Per iniziare a utilizzare {{site.data.keyword.messagehub}}
e a inviare e ricevere messaggi, puoi utilizzare l'esempio Java™. L'esempio mostra in che modo un produttore invia
i messaggi a un consumatore utilizzando un argomento. Viene utilizzato lo stesso programma di esempio sia per consumare che per produrre
i messaggi.

Per comprendere meglio la modalità di funzionamento di {{site.data.keyword.messagehub}}, vedi [Informazioni su {{site.data.keyword.messagehub}}](/docs/services/MessageHub/messagehub010.html).

Per accedere ad altri esempi di {{site.data.keyword.messagehub}}, compresi quelli per Node.js e Python, vedi la pagina degli [esempi di {{site.data.keyword.messagehub}} ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/ibm-messaging/message-hub-samples){:new_window}.

<!-- 11/01/18 - Karen - removing diagram as requested by James
![Java sample overview diagram](getting_started_sample.gif "Overview diagram of Java sample showing the flow of messages.")
-->

Completa la seguente procedura:
{: #getting_started_steps}
 
1. Crea un'istanza del servizio {{site.data.keyword.messagehub}}:

  a. Accedi a {{site.data.keyword.Bluemix_notm}} utilizzando l'interfaccia utente Web. 
  
  b. Fai clic su **CATALOGO**.
  
  c. Nella sezione **Servizi dell'applicazione**, seleziona **Piano Standard {{site.data.keyword.messagehub}}**. Viene visualizzata la pagina dell'istanza del servizio {{site.data.keyword.messagehub}}.
  
  d. Nel menu **Connetti a** lascia il servizio senza binding e immetti i nomi per il tuo servizio e le tue credenziali. Puoi utilizzare i valori predefiniti.
  
  e. Fai clic su **Crea**.

2. Se non li hai ancora, installa i seguenti prerequisiti:

    * [git ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://git-scm.com/){:new_window}
	* [Gradle ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://gradle.org/){:new_window}
    * Java 8 o superiore
 
3. Clona il repository git message-hub-samples immettendo il seguente comando dalla riga di comando:

    <pre class="pre">
    git clone https://github.com/ibm-messaging/message-hub-samples.git
    </pre>
	{: codeblock}

4. Modifica la directory dell'esempio della console java immettendo il seguente comando:

    <pre class="pre">
    cd message-hub-samples/kafka-java-console-sample
    </pre>
	{: codeblock}

5. Esegui questi comandi build:

    <pre class="pre">
    gradle clean && gradle build
    </pre>
	{: codeblock}

6. Avvia il consumatore sulla tua console immettendo il seguente comando:

    <pre class="pre">java -jar build/libs/kafka-java-console-sample-2.0.jar 
	<var class="keyword varname">kafka_brokers_sasl</var> <var class="keyword varname">kafka_admin_url</var> token<var class="keyword varname">:api_key</var> -consumer</pre>
    {: codeblock}
    
    L'esempio utilizza un argomento denominato `kafka-java-console-sample-topic`. Se l'argomento non esiste
    già, viene creato dall'esempio utilizzando l'API di amministrazione {{site.data.keyword.messagehub}}. Per inviare e ricevere i
    messaggi, l'esempio usa l'API Java Apache Kafka.

    Per trovare i valori di *kafka_brokers_sasl*, *kafka_admin_url*
    e *api_key*, vai alla tua istanza di {{site.data.keyword.messagehub}} in {{site.data.keyword.Bluemix_notm}}, passa alla scheda **Credenziali del servizio** e seleziona le **Credenziali** che vuoi utilizzare.
	
	Specifica <code>token</code> come tuo nome utente e la <var class="keyword varname">api_key</var> come tua password. Separa <code>token</code> e la <var class="keyword varname">api_key</var> con un carattere due punti.
    
	**Importante:** *kafka_brokers_sasl* deve essere una singola stringa e deve essere racchiusa tra virgolette. Ad esempio:

    <pre class="pre">
    "host1:port1,host2:port2"
    </pre>
	{: codeblock}

    Si consiglia di utilizzare tutti gli host Kafka elencati nelle **Credenziali** che hai selezionato.

7. Avvia il produttore sulla tua console immettendo il seguente comando:
   
    <pre class="pre">java -jar build/libs/kafka-java-console-sample-2.0.jar 
	<var class="keyword varname">kafka_brokers_sasl</var> <var class="keyword varname">kafka_admin_url</var> token<var class="keyword varname">:api_key</var> -producer</pre>
 {: codeblock}
  
8. Dovresti ora vedere i messaggi inviati dal produttore che compaiono nel consumatore. Di seguito è
riportato un output di esempio:

    ```
    [2018-07-02 14:54:50,788] INFO Running in local mode. (com.messagehub.samples.MessageHubConsoleSample)
    [2018-07-02 14:54:50,789] INFO Kafka Endpoints: kafka-0.mh-zarjkgtnzzspbkfrkqgdhmq.us-south.containers.appdomain.cloud:9093,kafka-1.mh-zarjkgtnzzspbkfrkqgdhmq.us-south.containers.appdomain.cloud:9093,kafka-2.mh-zarjkgtnzzspbkfrkqgdhmq.us-south.containers.appdomain.cloud:9093 (com.messagehub.samples.MessageHubConsoleSample)
    [2018-07-02 14:54:50,789] INFO Admin REST Endpoint: https://mh-zarjkgtnzzspbkfrkqgdhmq.us-south.containers.appdomain.cloud (com.messagehub.samples.MessageHubConsoleSample)
    [2018-07-02 14:54:50,789] INFO Creating the topic kafka-java-console-sample-topic (com.messagehub.samples.MessageHubConsoleSample)
    [2018-07-02 14:54:52,680] INFO Admin REST response : (com.messagehub.samples.MessageHubConsoleSample)
    [2018-07-02 14:54:53,351] INFO Admin REST Listing Topics: [{"name":"kafka-java-console-sample-topic","partitions":1,"retentionMs":86400000,"cleanupPolicy":"delete"},{"name":"__consumer_offsets","partitions":50,"retentionMs":86400000,"cleanupPolicy":"compact"}] (com.messagehub.samples.MessageHubConsoleSample)
    [2018-07-02 14:54:55,126] INFO [Partition(topic = kafka-java-console-sample-topic, partition = 0, leader = 0, replicas = [0,2,1], isr = [0,2,1], offlineReplicas = [])] (com.messagehub.samples.ConsumerRunnable)
    [2018-07-02 14:54:55,126] INFO class com.messagehub.samples.ConsumerRunnable is starting. (com.messagehub.samples.ConsumerRunnable)
    [2018-07-02 14:54:56,328] INFO [Partition(topic = kafka-java-console-sample-topic, partition = 0, leader = 0, replicas = [0,2,1], isr = [0,2,1], offlineReplicas = [])] (com.messagehub.samples.ProducerRunnable)
    [2018-07-02 14:54:56,328] INFO MessageHubConsoleSample will run until interrupted. (com.messagehub.samples.MessageHubConsoleSample)
    [2018-07-02 14:54:56,328] INFO class com.messagehub.samples.ProducerRunnable is starting. (com.messagehub.samples.ProducerRunnable)
    [2018-07-02 14:54:57,514] INFO Message produced, offset: 0 (com.messagehub.samples.ProducerRunnable)
    [2018-07-02 14:54:59,652] INFO Message produced, offset: 1 (com.messagehub.samples.ProducerRunnable)
    [2018-07-02 14:55:00,671] INFO No messages consumed (com.messagehub.samples.ConsumerRunnable)
    [2018-07-02 14:55:01,788] INFO Message produced, offset: 2 (com.messagehub.samples.ProducerRunnable)
    [2018-07-02 14:55:01,797] INFO Message consumed: ConsumerRecord(topic = kafka-java-console-sample-topic, partition = 0, offset = 2, CreateTime = 1530539701655, serialized key size = 3, serialized value size = 25, headers = RecordHeaders(headers = [], isReadOnly = false), key = key, value = This is a test message #2) (com.messagehub.samples.ConsumerRunnable)
    [2018-07-02 14:55:03,921] INFO Message consumed: ConsumerRecord(topic = kafka-java-console-sample-topic, partition = 0, offset = 3, CreateTime = 1530539703789, serialized key size = 3, serialized value size = 25, headers = RecordHeaders(headers = [], isReadOnly = false), key = key, value = This is a test message #3) (com.messagehub.samples.ConsumerRunnable)
    [2018-07-02 14:55:03,921] INFO Message produced, offset: 3 (com.messagehub.samples.ProducerRunnable)
    [2018-07-02 14:55:06,053] INFO Message consumed: ConsumerRecord(topic = kafka-java-console-sample-topic, partition = 0, offset = 4, CreateTime = 1530539705922, serialized key size = 3, serialized value size = 25, headers = RecordHeaders(headers = [], isReadOnly = false), key = key, value = This is a test message #4) (com.messagehub.samples.ConsumerRunnable)
    [2018-07-02 14:55:06,054] INFO Message produced, offset: 4 (com.messagehub.samples.ProducerRunnable)
    [2018-07-02 14:55:08,186] INFO Message consumed: ConsumerRecord(topic = kafka-java-console-sample-topic, partition = 0, offset = 5, CreateTime = 1530539708055, serialized key size = 3, serialized value size = 25, headers = RecordHeaders(headers = [], isReadOnly = false), key = key, value = This is a test message #5) (com.messagehub.samples.ConsumerRunnable)
    ```
	{: codeblock}
	
9. L'esempio viene eseguito indefinitamente finché non viene arrestato. Per arrestare il processo, esegui un comando simile
a questo: <code>Ctrl+C</code>

<!-- 07/06/18 - Karen: removing until a newer version available
To watch a video that walks
you through getting a Java sample to run against {{site.data.keyword.messagehub}}, see [{{site.data.keyword.messagehub}} - Getting started with IBM's Kafka in the cloud ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.youtube.com/watch?v=tt-bLtFzC_4){:new_window}.
-->


