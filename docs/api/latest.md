# API Docs - v2.0.3

## Sinkmapper

### keyvalue *<a target="_blank" href="https://siddhi.io/en/v5.0/docs/query-guide/#sink-mapper">(Sink Mapper)</a>*

<p style="word-wrap: break-word">The <code>Event to Key-Value Map</code> output mapper extension allows you to convert Siddhi events processed by WSO2 SP to key-value map events before publishing them. You can either use pre-defined keys where conversion takes place without extra configurations, or use custom keys with which the messages can be published.</p>

<span id="syntax" class="md-typeset" style="display: block; font-weight: bold;">Syntax</span>
```
@sink(..., @map(type="keyvalue")
```

<span id="examples" class="md-typeset" style="display: block; font-weight: bold;">Examples</span>
<span id="example-1" class="md-typeset" style="display: block; color: rgba(0, 0, 0, 0.54); font-size: 12.8px; font-weight: bold;">EXAMPLE 1</span>
```
@sink(type='inMemory', topic='stock', @map(type='keyvalue'))
define stream FooStream (symbol string, price float, volume long);

```
<p style="word-wrap: break-word">This query performs a default Key-Value output mapping. The expected output is something similar to the following:symbol:'WSO2'<br>price : 55.6f<br>volume: 100L</p>

<span id="example-2" class="md-typeset" style="display: block; color: rgba(0, 0, 0, 0.54); font-size: 12.8px; font-weight: bold;">EXAMPLE 2</span>
```
@sink(type='inMemory', topic='stock', @map(type='keyvalue', @payload(a='symbol',b='price',c='volume')))
define stream FooStream (symbol string, price float, volume long);

```
<p style="word-wrap: break-word">This query performs a custom Key-Value output mapping where values are passed as objects. Values for <code>symbol</code>, <code>price</code>, and <code>volume</code> attributes are published with the keys <code>a</code>, <code>b</code> and <code>c</code> respectively. The expected output is a map similar to the following:<br>a:'WSO2'<br>b : 55.6f<br>c: 100L</p>

<span id="example-3" class="md-typeset" style="display: block; color: rgba(0, 0, 0, 0.54); font-size: 12.8px; font-weight: bold;">EXAMPLE 3</span>
```
@sink(type='inMemory', topic='stock', @map(type='keyvalue', @payload(a='{{symbol}} is here',b='`price`',c='volume')))
define stream FooStream (symbol string, price float, volume long);

```
<p style="word-wrap: break-word">This query performs a custom Key-Value output mapping where the values of the <code>a</code> and <code>b</code> attributes are strings and c is object. The expected output should be a Map similar to the following:a:'WSO2 is here'<br>b : 'price'<br>c: 100L</p>

## Sourcemapper

### keyvalue *<a target="_blank" href="https://siddhi.io/en/v5.0/docs/query-guide/#source-mapper">(Source Mapper)</a>*

<p style="word-wrap: break-word"><code>Key-Value Map to Event</code> input mapper extension allows transports that accept events as key value maps to convert those events to Siddhi events. You can either receive pre-defined keys where conversion takes place without extra configurations, or use custom keys to map from the message.</p>

<span id="syntax" class="md-typeset" style="display: block; font-weight: bold;">Syntax</span>
```
@source(..., @map(type="keyvalue", fail.on.missing.attribute="<BOOL>")
```

<span id="query-parameters" class="md-typeset" style="display: block; color: rgba(0, 0, 0, 0.54); font-size: 12.8px; font-weight: bold;">QUERY PARAMETERS</span>
<table>
    <tr>
        <th>Name</th>
        <th style="min-width: 20em">Description</th>
        <th>Default Value</th>
        <th>Possible Data Types</th>
        <th>Optional</th>
        <th>Dynamic</th>
    </tr>
    <tr>
        <td style="vertical-align: top">fail.on.missing.attribute</td>
        <td style="vertical-align: top; word-wrap: break-word"> If this parameter is set to <code>true</code>, if an event arrives without a matching key for a specific attribute in the connected stream, it is dropped and not processed by the Stream Processor. If this parameter is set to <code>false</code> the Stream Processor adds the required key to such events with a null value, and the event is converted to a Siddhi event so that you could handle them as required before they are further processed.</td>
        <td style="vertical-align: top">true</td>
        <td style="vertical-align: top">BOOL</td>
        <td style="vertical-align: top">Yes</td>
        <td style="vertical-align: top">No</td>
    </tr>
</table>

<span id="examples" class="md-typeset" style="display: block; font-weight: bold;">Examples</span>
<span id="example-1" class="md-typeset" style="display: block; color: rgba(0, 0, 0, 0.54); font-size: 12.8px; font-weight: bold;">EXAMPLE 1</span>
```
@source(type='inMemory', topic='stock', @map(type='keyvalue'))
define stream FooStream (symbol string, price float, volume long);

```
<p style="word-wrap: break-word">This query performs a default key value input mapping. The expected input is a map similar to the following:<br>symbol: 'WSO2'<br>price: 55.6f<br>volume: 100</p>

<span id="example-2" class="md-typeset" style="display: block; color: rgba(0, 0, 0, 0.54); font-size: 12.8px; font-weight: bold;">EXAMPLE 2</span>
```
@source(type='inMemory', topic='stock', @map(type='keyvalue', fail.on.missing.attribute='true', @attributes(symbol = 's', price = 'p', volume = 'v')))define stream FooStream (symbol string, price float, volume long); 
```
<p style="word-wrap: break-word">This query performs a custom key value input mapping. The matching keys for the <code>symbol</code>, <code>price</code> and <code>volume</code> attributes are be <code>s</code>, <code>p, and </code>v` respectively.  The expected input is a map similar to the following:
s: 'WSO2'
p: 55.6
v: 100</p>

