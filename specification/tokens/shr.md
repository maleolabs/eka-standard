# Token: shr- — Sharing Object

- **Token ID:** `shr-`
- **Artifact Type:** Sharing Object
- **Knowledge Dimension:** records
- **Engineering Domain:** Operations (stratum 5)
- **Owned State Domains:** Content State, Existence State
- **Identity/relationship notes:** IsKnowledge true. A snapshot copy derived from a source CKO at release time; never a live projection. Acuan: ADR sharing-object-model.

## Required fields

| Field | Type | Required | Notes |
| ----- | ---- | -------- | ----- |
| title | string | yes | Judul paket sharing, non-empty. |
| description | string | yes | Deskripsi isi dan tujuan paket, non-empty. |
| level | enum `L0\|L1\|L2` | yes | Kedalaman opt-in, lihat Levels. |
| provenance | enum `extracted\|audited` | yes | MVP: `extracted` only. |
| sourceHash | string | yes | Pin `objectHash` sumber saat rilis. |
| sourceRef | relationship `derives-from` | yes | Target `rel:` versi (`rel:<id>:<versi>`). |

## Levels (normative, opt-in)

- **L0** — metadata only: title, description, sourceRef, sourceHash. Tanpa konten sumber.
- **L1** — L0 + ringkasan/struktur aman: ringkasan dan struktur tanpa konten sensitif.
- **L2** — L1 + snapshot konten penuh: salinan konten sumber pada `sourceHash`.

Level dipilih eksplisit per rilis. Default-deny: tanpa level eksplisit, tidak ada yang dibagikan.

## Provenance

- `extracted` — hasil builder ekstrak CKO (MVP, EKA-to-EKA).
- `audited` — hasil audit, dicadangkan; belum normatif di MVP.

## Relationship rules

- MUST carry `derives-from` ke `rel:` versi.
- MUST NOT carry `depends-on` live ke sumber.
- Versioning per `rel`: rilis baru = instance baru + `derives-from` baru.

## Snapshot + pin-hash

Konten shr adalah salinan beku saat rilis. `sourceHash` pin `objectHash` sumber. Konsumen fetch tanpa repo sumber.

## Opt-in default-deny

Default share nothing. Berbagi hanya field yang tercakup level eksplisit.
