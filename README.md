# Messaging
Enterprise Java Bean (*EJB*) Message Driven Bean (*MDB*) that consumes from **MQ** and passes the contents of the message to a notification service.

This *MDB* responds to the **JMS** *TextMessage*s that the *portfolio* microservice delivers to **MQ** whenever a portfolio changes levels, such as from *Silver* to *Gold*.

Note that this is the only microservice in the **Stock Trader** sample that uses the traditional **Java EE** programming model (*EJB*s, *JMS*, *JNDI*, etc.).  Due to this, it is also the only one that depends on the full `websphere-liberty:javaee8` Docker image (as opposed to the others that just need `websphere-liberty:microProfile2`).

This *MDB* expects to receive a *TextMessage* containing a *JSON* object with four fields: `id`, `owner`, `old`, and `new`.  For example, you could post a message like `{"id": "jalcorn@us.ibm.com", "owner": "John", "old": "Silver", "new": "Gold"}` to its **MQ** queue, and it will pass that JSON object to the *notification* microservice.  There are multiple versions of the *notification* service; one posts a message to **Slack** (the *#stock-trader-messages* channel on *ibm-cloud.slack.com*), and another sends a tweet to **Twitter** (the *@IBMStockTrader* account).
