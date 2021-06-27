# Troubleshooting

If your node is in go-lachesis 1.0.0-rc0, and you still have events before migration \(block 4564024\), then you have two options:

1. Run the node in rc0 version and let the node complete the migration \(it takes 1hr or more depending on the machine specs\). You can check your log to see the progress. After migration, the node will run normal.
2. 
If the node was migrated successfully \(check the log\), then:

* You can simply run in rc0 like before.

If the node failed the migration for whatever reason \(check the log\), then:

* You will need to run the node in rc1. See the instruction above \(option 2\).

