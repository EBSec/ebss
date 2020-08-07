<h1>Enterprise Blockchain Security Specification</h1>


<p><b>Version 1.0.0

<h2>About</h2>


The Enterprise Blockchain Security Specification (EBSS) is a specification aimed at fomenting a minimum standard of security for enterprise applications that make use of / or interact with a distributed ledger system, which may include both public and permissioned blockchains. The specification includes a list of requirements that SHOULD be fulfilled by such an enterprise blockchain application. It is inspired by the [Cryptocurrency Security Standards (CCSS)](https://cryptoconsortium.github.io/CCSS/) but caters to more complex applications that involve enterprise logic, tokenization solutions, and smart contracts. 

<h2>Disclaimer</h2>


THE CONTENT OF THIS SPECIFICATION IS PROVIDED “AS IS”, WITHOUT REPRESENTATIONS AND WARRANTIES OF ANY KIND.

THE AUTHOR AND HIS EMPLOYER DISCLAIM ANY LIABILITY FOR DAMAGE ARISING OUT OF, OR IN CONNECTION WITH THE APPLICATION OF THIS STANDARD.

<h2>Scope</h2>


The EBSS SHOULD not be considered a replacement for CCSS and SHOULD be seen as complementary to existing information security standards, such as [ISO/IEC 27001:2013](https://www.iso.org/standard/54534.html). It covers best practices and organizational security policies in the design and deployment of enterprise blockchain applications, in areas, such as key generation and storage, user privacy, and administrative policies.

However, the specification does not cover details of cryptographic implementations, secure coding patterns, and specific node configurations. It also does not consider the caveats of specific distributed ledger platforms and the details of their configuration. 

<h2>Specification</h2>


The words “MUST”, “MUST NOT”, “REQUIRED”, “SHALL”, “SHALL NOT”, “SHOULD”, “SHOULD NOT”, “RECOMMENDED”, “MAY”, and “OPTIONAL” in this document are to be interpreted as described in [RFC 2119](https://tools.ietf.org/html/rfc2119#:~:text=Authors%20who%20follow%20these%20guidelines,as%20described%20in%20RFC%202119.).

<h3>Key Management</h3>


<h4>Key Generation</h4>



<table>
  <tr>
   <td><strong>R1.1.1</strong>
   </td>
   <td><strong>Cryptographically Secure Randomness</strong>
   </td>
   <td>All keys MUST be created from a cryptographically secure source of randomness according to common cryptographic standards.
   </td>
  </tr>
  <tr>
   <td><strong>R1.1.2</strong>
   </td>
   <td><strong>Trusted Key Creation Environment</strong>
   </td>
   <td>Keys MUST be created in a trusted environment. In the context of normal user keys, this means they MUST be created either on the machine controlled by the user of an environment local to the key creator and storage process. Alternatively, they can be generated within a trusted execution environment (TEE) or a special purpose hardware security module (HSM). 
   </td>
  </tr>
  <tr>
   <td><strong>R1.1.3</strong>
   </td>
   <td><strong>Key Derivation Functions</strong>
   </td>
   <td>Keys derived from a password MUST use a cryptographically secure and preferably standardized key derivation function configured to use standard recommended parameters. For instance, in the case of PBKDF2HMAC, the <a href="https://pages.nist.gov/800-63-3/sp800-63b.html">NIST recommendation</a> of using 128-bit long salt values SHOULD be used. 
   </td>
  </tr>
  <tr>
   <td><strong>R1.1.4</strong>
   </td>
   <td><strong>Secure Key Delivery</strong>
   </td>
   <td>Keys generated on behalf of a user MUST be delivered over a secure channel or offline. This means, they may be sent over an encrypted communication channel with secure authentication, but not via standard email or similar unencrypted channels. 
   </td>
  </tr>
</table>


<h4>Key Storage</h4>



<table>
  <tr>
   <td><strong>R1.2.1</strong>
   </td>
   <td><strong>Encrypted Key Storage</strong>
   </td>
   <td>All keys MUST be encrypted using a standard encryption algorithm when stored on a digital storage medium.
   </td>
  </tr>
  <tr>
   <td><strong>R1.2.2</strong>
   </td>
   <td><strong>Disconnected Storage for Critical Interactive Keys</strong>
   </td>
   <td>Keys that control significant assets or critical operations and are to be used by an operator interactively, MUST be in cold storage when not used, preferably in a hardware wallet that has to be connected for specific uses.  
   </td>
  </tr>
  <tr>
   <td><strong>R1.2.3</strong>
   </td>
   <td><strong>Node Software  Key Store </strong>
   </td>
   <td>Keys MUST not be stored in the blockchain platform’s in-node wallet. Instead, keys SHOULD be stored in encrypted format in a separate location and raw transactions SHOULD be processed by the node, meaning the transactions are not signed by the node software itself.
   </td>
  </tr>
</table>


<h4>Key Usage Protocol</h4>



<table>
  <tr>
   <td><strong>R1.3.1</strong>
   </td>
   <td><strong>Automated Key Use</strong>
   </td>
   <td>All keys used for automated processes in so-called hot wallets MUST be stored in a trusted system, in encrypted form. These “hot wallets” SHOULD be covered by real-time monitorization, if significant funds are involved.
   </td>
  </tr>
  <tr>
   <td><strong>R1.3.2</strong>
   </td>
   <td><strong>Administrative Keys</strong>
   </td>
   <td>All administrative keys MUST be issued to trusted personnel only and issuance MUST be accounted for (recorded). 
   </td>
  </tr>
  <tr>
   <td><strong>R1.3.3</strong>
   </td>
   <td><strong>Key Usage Logging</strong>
   </td>
   <td>Every use of a critical key (administrative key) MUST be logged.
   </td>
  </tr>
  <tr>
   <td><strong>R1.3.4</strong>
   </td>
   <td><strong>Multi-sig</strong>
   </td>
   <td>In the case of keys dealing with highly sensitive operations, such as upgrading a smart contract or modifying important parameters, a multi-signature scheme SHOULD be considered.
   </td>
  </tr>
</table>


<h4>Key Recovery</h4>



<table>
  <tr>
   <td><strong>R1.4.1</strong>
   </td>
   <td><strong>HD-Wallets </strong>
   </td>
   <td>In the case of using hierarchical deterministic key generation  (for example <a href="https://github.com/bitcoin/bips/blob/master/bip-0032.mediawiki">BIP 32</a>) a clear process MUST be defined on how seed words are stored offline for internal users. Clear guidance MUST be given to external users on seed word security.
   </td>
  </tr>
  <tr>
   <td><strong>R1.4.2</strong>
   </td>
   <td><strong>Seed Backups</strong>
   </td>
   <td>Seed words, passphrases used for key recovery, and any other material that may serve to recover keys MUST be backed up securely offline. 
   </td>
  </tr>
  <tr>
   <td><strong>R1.4.3</strong>
   </td>
   <td><strong>Key Compromise Protocol</strong>
   </td>
   <td>A document describing the process executed in the case a key is compromised MUST exist and cover: compromise communication procedure, key revocation, issuance of replacement keys
   </td>
  </tr>
</table>


<h3>Operational Policy </h3>


<h4>Node Operation</h4>



<table>
  <tr>
   <td><strong>R2.1.1</strong>
   </td>
   <td><strong>Backup Nodes</strong>
   </td>
   <td>In the case of the blockchain application interfacing with a public blockchain, the company SHOULD run a full node of the blockchain in question, in order to have a full local backup of the data.
   </td>
  </tr>
  <tr>
   <td><strong>R2.1.2</strong>
   </td>
   <td><strong>Gateway Redundancy </strong>
   </td>
   <td>In the case of interfacing with a public blockchain, at least one backup access MUST be used. For example, the own node a company operates SHOULD be backed up by a public access gateway, to ensure continuous operation. 
   </td>
  </tr>
</table>


<h4>IT Security</h4>



<table>
  <tr>
   <td><strong>R2.2.1</strong>
   </td>
   <td><strong>Data Sanitization Policy </strong>
   </td>
   <td>The company MUST have a clearly defined policy on how sensitive data is removed from storage media when equipment is retired or leaves the company.
   </td>
  </tr>
  <tr>
   <td><strong>R2.2.2</strong>
   </td>
   <td><strong>Credentials Management </strong>
   </td>
   <td>A clear policy MUST exist on how credentials are issued and revoked in the company. 
   </td>
  </tr>
</table>


<h3>User Privacy</h3>



<table>
  <tr>
   <td><strong>R3.1.1</strong>
   </td>
   <td><strong>Address Re-use</strong>
   </td>
   <td>Addresses on public blockchains for users MUST not be re-used between different applications, unless unavoidable because of the application logic. The purpose of this is to avoid correlation. All external users SHOULD be advised not to use their addresses for other applications. 
   </td>
  </tr>
  <tr>
   <td><strong>R3.1.2</strong>
   </td>
   <td><strong>Personal Data </strong>
   </td>
   <td>No personal data MUST be stored directly on a public or private blockchain if the data allows identifying the user. Instead, this type of data SHOULD be stored off-chain and be cryptographically linked (hash-timestamped) onto the blockchain.
   </td>
  </tr>
</table>


<h3>Smart Contract Security</h3>



<table>
  <tr>
   <td><strong>R4.1.1</strong>
   </td>
   <td><strong>External Audits</strong>
   </td>
   <td>All smart contracts that are deployed on a public blockchain MUST be audited by an external security firm. 
   </td>
  </tr>
  <tr>
   <td><strong>R4.1.2</strong>
   </td>
   <td><strong>Contract Monitorization</strong>
   </td>
   <td>Smart contracts that hold significant value SHOULD be monitored in real-time.
   </td>
  </tr>
</table>

