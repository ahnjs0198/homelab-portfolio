# Incident notes

These are historical observations from the October operations record.

## Overlay interruption and certificate renewal failure · October 26–27, 2026

- **Observed:** Tailscale node keys expired on Server1 and Pi-hole. Server1's resolver pointed at overlay DNS, so loss of the overlay also broke DNS resolution. Caddy certificate renewal failed.
- **Response:** Restored the OS-managed resolver on Server1, reauthenticated the overlay nodes, and restarted Caddy. Tailnet DNS was subsequently updated to use the re-registered Pi-hole.
- **Result:** The October 27 check recorded renewed certificates. The design lesson was to keep host resolution functional during an overlay outage.

## Cloudflare 522 responses and a blank blog page · October 27, 2026

- **Observed:** Several public names still pointed to a retired public address and returned Cloudflare 522. The blog had a separate problem: Caddy was missing the HTTP origin route expected by the tunnel.
- **Response:** Replaced stale DNS records with tunnel records and corrected Caddy's origin routing and proxy handling.
- **Result:** The five affected or checked site names responded through Cloudflare after the changes. The blog and Nextcloud login redirects retained HTTPS. The blog still ran WordPress at the time.
- **Lesson:** Check DNS, edge reachability, origin routing, and application redirects separately. An edge error and an origin routing fault can occur during the same migration.

## Competing DHCP servers · October 27, 2026

- **Observed:** The gateway and Pi-hole had both issued leases, so DNS assignment differed between clients.
- **Response:** Disabled gateway DHCP and checked the DHCP discovery response.
- **Result:** Pi-hole was the only responder in the test. The gateway still advertised IPv6 DNS. A desktop-side adjustment was verified, with wider client coverage unresolved.

[Back to overview](../README.md)
