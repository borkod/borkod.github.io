# Azure Global Load Balancing Comparison

Global load-balancing services distribute traffic across applications
and endpoints hosted across different regions/geographies. These
services route end-user traffic to the available backend based on
configurable routing rules. They also feature endpoint monitoring in
order to improve high availability and reliability of backend services.
Azure offers two global load-balancing services: Azure Traffic Manager
and Azure Front Door.

[Traffic
Manager](https://docs.microsoft.com/en-us/azure/traffic-manager/) is a
DNS-based traffic load balancer that distributes traffic to services
across global Azure regions. Being a DNS-based load-balancing service,
it load balances only at the domain level. As such, it supports any
communication protocol and has no performance impact.

[Front Door](https://docs.microsoft.com/en-us/azure/frontdoor/) is
global load balancing service specifically designed for web
applications. Therefore, it works at Layer 7 and offers many
capabilities useful for web-based application (e.g SSL offloading,
path-based routing, fast fail-over, caching, WAF, etc.)

I thought it would be useful to compile a list of features offered by
the two services so that they can be easily and quickly compared and
contrasted. Azure documentation offers a very practical [decision
tree](https://docs.microsoft.com/en-us/azure/architecture/guide/technology-choices/load-balancing-overview#decision-tree-for-load-balancing-in-azure)
that's great for determining the right load-balancing solution for
various scenarios. I hope the table below is helpful!

<table>
<col width="33%" />
<col width="33%" />
<col width="33%" />
<thead>
<tr class="header">
<th align="left">Feature</th>
<th align="left">Traffic Manager</th>
<th align="left">Front Door</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">Protocol</td>
<td align="left">Protocol Agnostic (DNS based)</td>
<td align="left">HTTP(S)</td>
</tr>
<tr class="even">
<td align="left">Protocol Support: HTTP/2</td>
<td align="left">✔️</td>
<td align="left">✔️</td>
</tr>
<tr class="odd">
<td align="left">Protocol Suppport: IPv6</td>
<td align="left">✔️</td>
<td align="left">✔️</td>
</tr>
<tr class="even">
<td align="left">Supported Backends<sup><a href="#fn:1">1</a></sup></td>
<td align="left"><ul>
<li>Any public IP or a publicly resolvable DNS hostname</li>
<li>Nested endpoints (used to combine Traffic Manager profiles)</li>
</ul></td>
<td align="left">Any public IP or a publicly resolvable DNS hostname</td>
</tr>
<tr class="odd">
<td align="left">Non-Azure Backends</td>
<td align="left">✔️</td>
<td align="left">✔️</td>
</tr>
<tr class="even">
<td align="left">Backend must be public</td>
<td align="left">✔️</td>
<td align="left">✔️</td>
</tr>
<tr class="odd">
<td align="left">Nesting</td>
<td align="left">✔️</td>
<td align="left">❌</td>
</tr>
<tr class="even">
<td align="left">Endpoint Monitoring</td>
<td align="left">✔️</td>
<td align="left">✔️</td>
</tr>
<tr class="odd">
<td align="left">Fast Fail-over</td>
<td align="left">❌<sup><a href="#fn:2">2</a></sup></td>
<td align="left">✔️</td>
</tr>
<tr class="even">
<td align="left">Routing Methods</td>
<td align="left"><ul>
<li>Performance routing</li>
<li>Priority routing</li>
<li>Weighted round-robin routing</li>
<li>Geographic routing</li>
<li>Multivalue</li>
<li>Subnet routing</li>
</ul></td>
<td align="left"><ul>
<li>Latency Routing</li>
<li>Priority Routing</li>
<li>Weighted Routing</li>
<li>Geographic Routing (vai WAF policy)</li>
</ul></td>
</tr>
<tr class="odd">
<td align="left">HTTP Property Routing</td>
<td align="left">❌</td>
<td align="left">✔️</td>
</tr>
<tr class="even">
<td align="left">Session Affinity</td>
<td align="left">❌</td>
<td align="left">✔️</td>
</tr>
<tr class="odd">
<td align="left">TLS Termination</td>
<td align="left">❌</td>
<td align="left">✔️</td>
</tr>
<tr class="even">
<td align="left">Custom Domain</td>
<td align="left">✔️<sup><a href="#fn:3">3</a></sup></td>
<td align="left">✔️</td>
</tr>
<tr class="odd">
<td align="left">Wildcard domains</td>
<td align="left">✔️</td>
<td align="left">✔️</td>
</tr>
<tr class="even">
<td align="left">Certificate Management</td>
<td align="left">❌</td>
<td align="left">✔️</td>
</tr>
<tr class="odd">
<td align="left">self-signed certificates</td>
<td align="left">✔️</td>
<td align="left">❌</td>
</tr>
<tr class="even">
<td align="left">HTTPS Redirection</td>
<td align="left">❌</td>
<td align="left">✔️</td>
</tr>
<tr class="odd">
<td align="left">Re-encryption</td>
<td align="left">❌<sup><a href="#fn:4">4</a></sup></td>
<td align="left">✔️<sup><a href="#fn:5">5</a></sup></td>
</tr>
<tr class="even">
<td align="left">WAF</td>
<td align="left">❌</td>
<td align="left">✔️</td>
</tr>
<tr class="odd">
<td align="left">DDoS</td>
<td align="left">❌</td>
<td align="left">✔️</td>
</tr>
<tr class="even">
<td align="left">Caching</td>
<td align="left">❌</td>
<td align="left">✔️</td>
</tr>
<tr class="odd">
<td align="left">Content Compression</td>
<td align="left">❌</td>
<td align="left">✔️</td>
</tr>
<tr class="even">
<td align="left">Session Affinity</td>
<td align="left">❌</td>
<td align="left">✔️</td>
</tr>
<tr class="odd">
<td align="left">URL Rewrite</td>
<td align="left">❌</td>
<td align="left">✔️</td>
</tr>
<tr class="even">
<td align="left">URL redirect</td>
<td align="left">❌</td>
<td align="left">✔️</td>
</tr>
<tr class="odd">
<td align="left">Traffic View Dashboard</td>
<td align="left">✔️<sup><a href="#fn:6">6</a></sup></td>
<td align="left">❌</td>
</tr>
<tr class="even">
<td align="left">No Performance Impact</td>
<td align="left">✔️<sup><a href="#fn:7">7</a></sup></td>
<td align="left">❌</td>
</tr>
<tr class="odd">
<td align="left">Pricing Considerations</td>
<td align="left"><ul>
<li>DNS queries received</li>
<li>Monitored endpoints</li>
<li>User Measurements</li>
<li>Traffic View Data points</li>
</ul></td>
<td align="left"><ul>
<li>Outbound data transfer</li>
<li>Inbound data transfer</li>
<li>Routing Rules</li>
<li>Custom Domains</li>
<li>WAF Service Fee</li>
<li>WAF Rulesets</li>
<li>WAF Custom Rules</li>
</ul></td>
</tr>
</tbody>
</table>

* * * * *

1.  -   Azure Endpoints (PaaS Cloud Services, Storage, Web Apps)
    -   Public IP Address Resources (e.g. VM's with public IPs or Azure
        Load Balancer)
    -   External Backends (Public IPv4/IPv6 addresses, FQDNs)

    [↩︎](#fnref:1)
2.  Traffic Manager fail over limited by DNS caching/TTL [↩︎](#fnref:2)

3.  Traffic Manager supports Custom Domain via CNAME or Alias Records.
    [↩︎](#fnref:3)

4.  Traffic Manager doesn't support TLS Termination, so re-encryption
    isn't necessary. [↩︎](#fnref:4)

5.  Front Door connections to the backend happen over public IP, so it
    is recommended that Front Door is configured to use HTTPS as the
    forwarding protocol. [↩︎](#fnref:5)

6.  Traffic Manager Traffic View provides a dashboard of user base
    regions and their traffic patterns. [↩︎](#fnref:6)

7.  Traffic Manager works at the DNS level. Client connections are
    direct to service endpoints, and so there is no performance impact
    incurred when using Traffic Manager. [↩︎](#fnref:7)
