# ip-allowlist-evaluator

Evaluate whether supplied client addresses belong to an explicit CIDR allowlist.

## Run

Python 3.8 or later; no third-party packages or cloud credentials are required.

```sh
python3 tool.py examples/input.json
cat examples/input.json | python3 tool.py -
python3 -m unittest -v
```

## Example

Input:

```json
{
  "allowlist": [
    "10.0.0.0/8"
  ],
  "clients": [
    "10.1.2.3",
    "192.0.2.5"
  ]
}
```

Result:

```json
{
  "clients": [
    {
      "address": "10.1.2.3",
      "allowed": true
    },
    {
      "address": "192.0.2.5",
      "allowed": false
    }
  ]
}
```

The command writes JSON to standard output. Exit 0 means evaluation completed;
a finding in the output may still require attention. Invalid input returns exit 2,
with an error on standard error and no result on standard output.

## Operational scope

An offline membership check; it does not configure a firewall or establish client identity.

The tool evaluates supplied data locally. It does not change hosts, deploy
resources, or establish production compliance. Example identifiers and observations
are test fixtures. Keep credentials and private inventory out of Git.

## Design and verification

See [NOTES.md](NOTES.md) for the input contract, verification, and integration notes.
Related utilities: [syslog-severity-summary](https://github.com/sal-s-root/syslog-severity-summary), [port-range-merger](https://github.com/sal-s-root/port-range-merger).
