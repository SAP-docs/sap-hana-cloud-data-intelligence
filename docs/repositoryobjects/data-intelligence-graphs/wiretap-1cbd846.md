<!-- loio1cbd846dfec24a5b8ecce4fa07100bd4 -->

# Wiretap

The Wiretap operator allows you to inspect messages that are transferred from one operator to another. This graph is a simple automatic game where two players, Jane and John, play against each other. At each round, having 13 games, each player picks one card out of a deck of cards numbered from 1 to 13 and the player who has the higher numbered card wins. The Wiretap operator is inserted in this graph to display both the card that each player picked and the result of each game.



<a name="loio1cbd846dfec24a5b8ecce4fa07100bd4__section_r3z_hyt_w2b"/>

## Configure and Run the Graph

Follow the steps below to run the example from the SAP Data Intelligence Modeler UI:

1.  Start the graph.
2.  Open the UI from the wiretap operator so that the games are monitored.

    For example, the following output may be displayed:

    ```
    [2018-06-25 12:26:55.237] {"demo.card":5,"demo.game":10,"demo.player":"donald","demo.round":1}
    [2018-06-25 12:26:55.237] {"demo.card":10,"demo.game":10,"demo.player":"hillary","demo.round":1}
    [2018-06-25 12:26:55.240] {"demo.game":10,"demo.round":1,"demo.winner":"hillary"}{"donald":5,"hillary":5}
    [2018-06-25 12:26:57.236] {"demo.card":2,"demo.game":11,"demo.player":"donald","demo.round":1}
    [2018-06-25 12:26:57.236] {"demo.card":1,"demo.game":11,"demo.player":"hillary","demo.round":1}
    [2018-06-25 12:26:57.236] {"demo.game":11,"demo.round":1,"demo.winner":"donald"}{"donald":6,"hillary":5}
    [2018-06-25 12:26:59.236] {"demo.card":6,"demo.game":12,"demo.player":"donald","demo.round":1}
    [2018-06-25 12:26:59.236] {"demo.card":2,"demo.game":12,"demo.player":"hillary","demo.round":1}
    [2018-06-25 12:26:59.237] {"demo.game":12,"demo.round":1,"demo.winner":"donald"}{"donald":7,"hillary":5}
    [2018-06-25 12:27:01.237] {"demo.card":4,"demo.game":13,"demo.player":"donald","demo.round":1}
    [2018-06-25 12:27:01.237] {"demo.card":12,"demo.game":13,"demo.player":"hillary","demo.round":1}
    [2018-06-25 12:27:01.237] {"demo.game":13,"demo.round":1,"demo.winner":"hillary"}{"donald":7,"hillary":6}
    ...
    ```


