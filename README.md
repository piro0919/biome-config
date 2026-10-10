# biome-config

Shared Biome rules for `piro0919` repositories. ESLint のリポジトリは [eslint-config](https://github.com/piro0919/eslint-config) を使う。

数字や Tailwind の値をその場で書くと、同じ寸法や長さがあちこちで少しずつずれていく。値には名前を付けて1か所に置き、
名前を通さずに書いたら lint で落とす。

## Usage

```bash
pnpm add -D github:piro0919/biome-config#v1.0.0
```

```json
{
  "extends": ["@piro0919/biome-config/biome", "@piro0919/biome-config/tailwind"]
}
```

`tailwind` は Tailwind を使うリポジトリだけ足す。最初は警告で入れ、警告を直し終えたら
`biome-error`・`tailwind-error` に替えて、落とす形に切り替える。

## What it does

- `biome` — 名前の無い数字を落とす（`style/noMagicNumbers`）。0・1・2・10・24・60 などは Biome が数字のまま許す
- `tailwind` — `[...]` に数字の入った値をじかに書いたクラスを落とす（GritQL の規則 `tailwind-arbitrary.grit`）。文字列の定数に入れたクラスも見る

## Notes

Biome は、読み込んだ設定の中の `plugins` の場所を、その設定のファイルからでなくプロジェクトから数える。
そのため `tailwind.json` は `./node_modules/@piro0919/biome-config/` の中の規則を指している。`biome.json` はプロジェクトの直下に置く。

## Release

タグ（`v1.0.0` など）を打って push する。使う側は Renovate がタグの更新を PR で出す。
