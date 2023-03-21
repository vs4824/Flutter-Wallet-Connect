# Flutter Wallet Connect

Wallet Connect client in dart highly inspired from wallet-connect-kotlin by Trust Wallet.

## Usage

   ```
   import 'package:wallet_connect/wallet_connect.dart';
   ```

1. Create instance of Wallet connect client and define callbacks.

   ```
   final wcClient = WCClient(
      onConnect: () {
        // Respond to connect callback
      },
      onDisconnect: (code, reason) {
        // Respond to disconnect callback
      },
      onFailure: (error) {
        // Respond to connection failure callback
      },
      onSessionRequest: (id, peerMeta) {
        // Respond to connection request callback
      },
      onEthSign: (id, message) {
        // Respond to personal_sign or eth_sign or eth_signTypedData request callback
      },
      onEthSendTransaction: (id, tx) {
        // Respond to eth_sendTransaction request callback
      },
      onEthSignTransaction: (id, tx) {
        // Respond to eth_signTransaction request callback
      },
    );
   ```

2. Create WCSession object from wc: uri.

   ```
   final session = WCSession.from(wcUri);
   ```
   
3. Create WCPeerMeta object containing metadata for your app.

   ```
   final peerMeta = WCPeerMeta(
        name: 'Example Wallet',
        url: 'https://example.wallet',
        description: 'Example Wallet',
        icons: [],
    );
   ```
   
4. Connect to a new session.

   ```
   wcClient.connectNewSession(session: session, peerMeta: peerMeta);
   ```
   
5. Or connect to a saved session (from step 8).

   ``` 
   wcClient.connectFromSessionStore(sessionStore);
   ```
   
6. Approve a session connection request.

   ```
   wcClient.approveSession(
        accounts: [], // account addresses
        chainId: 1, // chain id
    );
   ```
   
7. Or reject a session connection request.

   ```
   wcClient.rejectSession();
   ```
   
8. Get active session from sessionStore getter to save for later use.

   ```
   final sessionStore = wcClient.sessionStore;
   ```
   
9. Approve a sign transaction request by signing the transaction and sending the signed hex data.

   ```
   wcClient.approveRequest<String>(
        id: id,
        result: signedDataAsHex,
    );
   ```
   
10. Approve a send transaction request by sending the transaction hash generated from sending the transaction.

   ```
   wcClient.approveRequest<String>(
        id: id,
        result: transactionHash,
    );
   ```
   
11. Approve a sign request by sending the signed data hex generated.

   ```
   wcClient.approveRequest<String>(
        id: id,
        result: signedDataAsHex,
    );
   ```
   
12. Or reject any of the requests above by specifying request id.
 
   ```
   wcClient.rejectRequest(id: id);
   ```
   
13. Disconnect from a connected session locally.

   ```
   wcClient.disconnect();
   ```
   
14. Permanently close a connected session.

   ```
   wcClient.killSession();
   ```



