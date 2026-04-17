# Running the Bot

Nothing at the V2 strategy layer is Delta-DeFi-specific beyond selecting `delta-defi` as the connector. Follow the official [Hummingbot V2 Strategies guide](https://hummingbot.org/strategies/scripts/#script-examples) for the full flow.

### Short version

```
>>> create --v2-config [SCRIPT_NAME]
# Select a script from the list
# Follow prompts to set trading pair, order amounts, spreads, etc.
# Save the config

>>>start --v2 [SCRIPT_CONFIG_FILE]
```

### Selecting Delta-DeFi as the connector

In your script config, use the connector ID `delta-defi`:

```yaml
exchange: delta-defi
trading_pair: ADA-USDM
# remaining strategy params
```

### Stopping the bot

```
>>> stop
```

Open orders are cancelled as part of shutdown, subject to the usual Hummingbot cancel-all flow.
