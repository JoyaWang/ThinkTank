# EOS常见问题



Error: 3190000 block_log_exception: Block log exception: block log does not contain last irreversible block



o solve this issue, go to your home directory.

Navigate to `~/.local/share/eosio/nodeos`

Here you will see two files `config` and `data`.

Delete the data folder using `rm -rf data/` and start your nodeos again. Error should be gone.

**OR**

You can use `--hard-replay` to replay the blockchain to the last irreversible block.

If you don't mind losing accounts that you have created, the first method is the best, however, if you do not want to lose the current accounts, make sure to use the second method.