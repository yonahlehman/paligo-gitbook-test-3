# Source Code Storage and Retention Policy

Uploaded source code is stored only for the duration of the scan session.

Once the scan is complete, the system retains only limited metadata or a hash of the code, stored in encrypted form (AES-256 at rest, TLS 1.3 in transit). This metadata contains only non-reversible identifiers, making it impossible to reconstruct or infer the original source code.

During a re-scan, new results are compared against the stored metadata to identify any additional vulnerabilities.
