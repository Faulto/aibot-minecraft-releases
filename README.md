# AIBOT Minecraft releases

This public repository is the small, source-free release channel for the AIBOT Minecraft Runner
gateway. AIBOT installations read one fixed asset from the latest GitHub Release:

```text
https://github.com/Faulto/aibot-minecraft-releases/releases/latest/download/aibot-runner-component.json
```

The descriptor points to an immutable, anonymously readable multi-architecture image at
`ghcr.io/faulto/aibot-minecraft-gateway@sha256:…`. AIBOT validates the descriptor's fixed identity,
protocol contract, source revision, exact digest, and `linux/amd64` plus `linux/arm64` manifests
before registering it. Runners pull the digest-pinned image; they do not clone or build source.

## Release contents

Each `v<version>` release contains:

- `aibot-runner-component.json` — the narrow machine-readable import descriptor;
- `gateway-compatibility.md` — operator-facing protocol and runtime compatibility;
- `gateway.sbom.json` — Buildx SBOM attestation evidence;
- `gateway.provenance.json` — Buildx provenance attestation evidence; and
- `SHA256SUMS` — checksums for the four evidence files above.

The descriptor schema is documented at
[`schema/aibot-runner-component.schema.json`](schema/aibot-runner-component.schema.json). AIBOT's
consumer code remains the authority: it reconstructs a closed Runner component manifest from the
descriptor rather than accepting commands, mounts, environment names, or arbitrary package URLs
from this repository.

## Publication boundary

Releases are produced by the reviewed `pnpm release:publish` command in the private
`Faulto/aibot-minecraft` source repository. The publisher qualifies a clean, pushed source revision,
builds amd64 and arm64 images locally with SBOM/provenance attestations, pushes to GHCR, verifies the
exact digest anonymously, and only then creates the release here.

No source checkout, Minecraft/Microsoft token, gateway credential, registry credential, server
configuration, world data, account cache, or accepted Minecraft EULA belongs in this repository.
Public availability of metadata or container images does not grant an open-source license; each
descriptor records the package's reviewed license identity.

See [SECURITY.md](SECURITY.md) for private vulnerability reporting guidance.
