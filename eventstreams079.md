---

copyright:
  years: 2015, 2019
lastupdated: "2018-05-25"

keywords: IBM Event Streams, Kafka as a service, managed Apache Kafka

subcollection: eventstreams

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

<!-- 12/11/18: info moved to eventstreams075.md, moved because of doc app changes -->
# How to connect and authenticate
{: #mql_connect_authenticate}

** The MQ Light API is available as part of the Standard plan only.**
<br/>

To connect an app to the service, the app must use the <code>user</code>,
<code>password</code>, and <code>mqlight_lookup_url</code> details from the [VCAP_SERVICES environment variable](/docs/services/EventStreams?topic=eventstreams-connecting). Use the following guidance for your chosen language:
{: shortdesc}

**For Java**

If you specify ‘null’ as the endpointService parameter of the create() call, this instructs the
client to read the <code>user</code>, <code>password</code> and,
<code>mqlight_lookup_url</code> details from VCAP_SERVICES:

<pre>
<code>NonBlockingClient.create(null, new NonBlockingClientAdapter<Void>() {
    public void onStarted(NonBlockingClient client, Void context) {
        client.send("my/topic", "Hello World!", null);
    }
}, null);</code>
</pre>
{:codeblock}

<br>

**For Node.js**

Retrieve the <code>user</code>, <code>password</code>, and
<code>mqlight_lookup_url</code> details from VCAP_SERVICES and use them to create the client as
follows:

<pre>
<code>var services = JSON.parse(process.env.VCAP_SERVICES);
mqlightService = services['messagehub'][0];
opts.service = mqlightService.credentials.mqlight_lookup_url;
opts.user = mqlightService.credentials.user;
opts.password = mqlightService.credentials.password;
var mqlightClient = mqlight.createClient(opts, function(err) {
...</code>
</pre>
{:codeblock}

<br>

**For Ruby**

Retrieve the <code>user</code>, <code>password</code>, and
<code>mqlight_lookup_url</code> details from VCAP_SERVICES and use them to create the client as
follows:
<pre>
<code>vcap_services = JSON.parse(ENV['VCAP_SERVICES'])
conn_details = vcap_services['messagehub']
credentials = conn_details.first['credentials']
service = credentials['mqlight_lookup_url']
opts[:user] = credentials['user']
opts[:password] = credentials['password']
set :client, Mqlight::BlockingClient.new(service, opts)
...</code>
</pre>
{:codeblock}

<br>

**For Python**

Retrieve the <code>user</code>, <code>password</code>, and
<code>mqlight_lookup_url</code> details from VCAP_SERVICES and use them to create the client as
follows:
<pre>
<code>vcap_services = json.loads(os.environ.get('VCAP_SERVICES'))
conn_details = vcap_services['messagehub'][0]
service = str(conn_details['credentials']['mqlight_lookup_url'])
security_options = {
      'user': str(conn_details['credentials']['user']),
      'password': str(conn_details['credentials']['password'])
}
client = mqlight.Client(service=service, 
                        security_options=security_options,
                        on_started=on_started)</code>
</pre>
{:codeblock}

<br>

For more information about the {{site.data.keyword.mql}} APIs,
see: [{{site.data.keyword.mql}} developerWorks&reg; site ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/messaging/mq-light/){:new_window}.
