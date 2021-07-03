# DBReqair.jar User Guide

This tool is only for users who have downgraded the java-tron version to [GreatVoyage-v4.2.1\(Origen\)](https://github.com/tronprotocol/java-tron/releases/tag/GreatVoyage-v4.2.1) or [GreatVoyage-v4.2.0\(Plato\)](https://github.com/tronprotocol/java-tron/releases/tag/GreatVoyage-v4.2.0) from [GreatVoyage-v4.2.2\(Lucretius\)](https://github.com/tronprotocol/java-tron/releases/tag/GreatVoyage-v4.2.2) or other higher versions.

If users meet the above conditions, users need to execute the DBReqair.jar tool to repair the database before users can start FullNode.jar normally.

[https://github.com/tronprotocol/tools/releases/tag/v1.0.0](https://github.com/tronprotocol/tools/releases/tag/v1.0.0)

1. Download the “DBRepair.jar” and “repair.sh” from the tool homepage and place them in the same directory as “FullNode.jar”.
2. Go to the “FullNode.jar” directory and execute the “repair.sh” file:

```text
sh ./repair.sh
```

1. Open the log file “logs/tron.log” and wait for the execution to complete, you will see "Repairment completed!" in log output once execution is complete. \(DBRepair will automatically exit after the execution is completed\).
2. Now the repair of the database has been completed. users can start the node normally with the latest version [GreatVoyage-v4.2.2.1\(Epictetus\)](https://github.com/tronprotocol/java-tron/releases/tag/GreatVoyage-v4.2.2.1)

This tool only needs to be executed once.

![](https://cdn.readme.io/img/book-icon.svg?1625079683213) Updated 7 days ago

* [Table of Contents](dbreqair.jar-user-guide.md)
  * [Scope](dbreqair.jar-user-guide.md#scope)
  * [Tool Homepage:](dbreqair.jar-user-guide.md#tool-homepage)
  * [Steps](dbreqair.jar-user-guide.md#steps)
  * [Notes](dbreqair.jar-user-guide.md#notes)

