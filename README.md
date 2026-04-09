{
  "version": "4.2.0",
  "name": "ampetra_neural_router",
  "instructions": [
    {
      "name": "initializeRoutingVault",
      "docs": [
        "Initializes a new RWA energy allocation vault. Requires MPC-level admin signature."
      ],
      "accounts": [
        { "name": "vaultState", "isMut": true, "isSigner": false },
        { "name": "adminMpcAuth", "isMut": false, "isSigner": true },
        { "name": "systemProgram", "isMut": false, "isSigner": false }
      ],
      "args": [
        { "name": "gridCapacityMw", "type": "u64" },
        { "name": "targetApyBps", "type": "u32" },
        { "name": "volatilityClamp", "type": "u16" }
      ]
    },
    {
      "name": "executeMevBurnRoute",
      "docs": [
        "Extracts arbitrage yield from the physical grid delta, routes 20% to buy-and-burn $AMP."
      ],
      "accounts": [
        { "name": "treasuryPool", "isMut": true, "isSigner": false },
        { "name": "burnAddress", "isMut": true, "isSigner": false },
        { "name": "telemetryOracle", "isMut": false, "isSigner": false }
      ],
      "args": [
        { "name": "epochId", "type": "u64" },
        { "name": "yieldDeltaUsd", "type": "u64" }
      ]
    }
  ],
  "errors": [
    {
      "code": 6001,
      "name": "DrawdownGuardTriggered",
      "msg": "Volatility exceeded safety parameters. Execution halted."
    },
    {
      "code": 6002,
      "name": "InvalidMpcSignature",
      "msg": "7-of-9 MPC signature verification failed."
    }
  ]
}
