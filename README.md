# AZAL Store Desk — Tablet Search & Return Finder v9

**Status: Demo works locally. Real mode has the correct application-login screen but is still disabled until the shared backend is implemented and deployed. This build is not suitable for live AZAL stock.**

## Start the demo

1. Extract this ZIP.
2. On Windows, run `start-demo.bat` (Python is required). It opens `http://127.0.0.1:8019`.
3. Choose **Demo**, then **Choose account to open demo**, select a test account, and enter the workspace.
4. Use test data only.

## Why Real mode asks for username and password

Real mode now displays the normal application login form. It does not ask staff to enter a Supabase project URL or key. Those are backend deployment settings, not login credentials.

A project owner will need to provision the shared database/authentication service once (Supabase was the proposed free-tier option). Regular staff do not need individual Supabase accounts. After the backend, schema, secure account provisioning, role policies, inventory reads/writes and transaction-safe release/return operations are implemented and tested, the Real login will be enabled.

At present the Real sign-in button is disabled honestly: this prototype does not yet authenticate users against a shared backend or synchronize inventory between computers. Do not use it for live stock.

## Included test data and limitations

- 15,988 AMASIS test inventory rows and 10,066 part definitions.
- Test tags were generated because the source workbook did not include Tag No.
- Stock assignment is separate from physical Location; physical Location is blank pending manual verification.
- Multi-quantity source rows were interpreted as batch/lot under the discussed rules, but identity exceptions still need review.
- Tool rows have temporary test Tool PNs where the source lacks verified tool identifiers.
- Source serviceability, material class, expiry and calibration metadata are not verified production facts.
- Demo changes remain in this browser only and are not synchronized across computers.

## Next backend milestone

1. Database schema for part definitions, individual/batch stock, release/return transactions, users and audit events.
2. Real username/password authentication and Admin/Superuser/Staff/incoming permissions enforced server-side.
3. Atomic issue/return operations and append-only audit trail.
4. Excel import preview, validation, backup and rollback.
5. Shared reads/writes, synchronization, and tested backup/restore before enabling Real mode.


## V9 changes for tablet/phone testing

- Parts Inventory and Tools Inventory have separate search fields for Part Number, Serial Number, Description, Tag No and Lot/Batch; Tools also has Tool PN and Tool Code. Entered fields combine to narrow results.
- Parts Returns and Tool Returns have separate searchable fields for Release Number, Part Number, Serial Number, Description, Aircraft Registration and Technician. Fully returned releases remain searchable in History.
- Each new multi-item release gets one automatically generated transaction number shared by its lines: A000001 through A999999, then B000001 and onward (after Z, the sequence extends to AA, AB, etc.). Legacy demo release lines without a number get individual numbers on migration.
- Search panels and filters adapt to desktop, tablet and phone. Wide inventory tables remain horizontally scrollable on small screens to preserve legibility.

### Open the local demo on your tablet

1. Run `start-demo.bat` on the Windows computer. Keep the window/server running.
2. Connect the tablet to the same Wi-Fi network as that computer.
3. Find the computer's IPv4 address with `ipconfig` in Command Prompt.
4. On the tablet, open `http://COMPUTER-IP:8019`, replacing `COMPUTER-IP` with that IPv4 address (for example, `http://192.168.1.25:8019`).
5. If Windows asks, allow Python on the **Private network**. If it does not ask and the page cannot open, Windows Firewall may need a private-network rule for port 8019.

This LAN setup is only for checking the responsive interface. Demo data is stored in each device's own browser and is NOT shared/synchronized. Real mode still requires the online backend.
