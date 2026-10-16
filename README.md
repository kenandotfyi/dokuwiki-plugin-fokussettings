# Fokus Settings

Optional DokuWiki admin companion for the Fokus template. Open Admin → Fokus Settings or the wiki actions menu's Fokus Settings link.

- Appearance: light/dark colors, bundled or system fonts, typography, spacing, corner radii, and internal/external link styles. Missing page links have independent light/dark colors and underline style, defaulting to red with a dotted underline.
- Workspace: panes, pane width, dark mode availability, sidebar visibility, and regex exclusions.
- Integrations: adapter cards for Preview, Annotations, and KaTeX with controls for the Fokus adapters, plus a read-only Dependencies subsection for Move, Tags, and Page Health. Status is green when ready, red when not installed, and amber when disabled or unavailable. Plugin installation and activation remain in Extension Manager.

Install the `fokussettings` directory under `lib/plugins/`, alongside a Fokus template containing `settings-schema.php` and `appearance.php`. DokuWiki enables newly installed plugins by default. The core Configuration Manager must be available for saving. Fokus must be the active template to change settings here.

The plugin edits template configuration through DokuWiki's Configuration API. It has no independent settings store, performs no template file writes, respects protected configuration, and requires administrator privileges and a valid security token for every save/reset. All submitted fields are validated before configuration is written. Disabled/protected inputs cannot be changed. Color values accept an empty string or six-digit hex values. Live theme previews are not included.

Disabling/removing this companion leaves saved template appearance and workspace behavior active. Configuration Manager can still edit the settings. Restore defaults resets just the chosen section; existing wiki tabs need a reload after a save. Color fields left blank retain the template's light/dark defaults. Page Health's special link styles remain separate.

License: GPL-2.0, as supplied in LICENSE.

### Interwiki appearance

Appearance → Interwiki links discovers prefixes through DokuWiki's merged built-in/local interwiki definitions, including entries such as `zotero` and `wp`. Select a prefix to set separate light/dark text, hover text, background, and hover background colors, plus decoration, decoration style, font weight/style, and favicon visibility. Blank values use prefix defaults before falling back to existing stylesheet rules. Zotero's former stylesheet palette is now defined in the shared settings defaults: red text in both themes, with separate light/dark hover text and backgrounds. The controls display these defaults. Clear a value to restore its default; DokuWiki continues to supply favicons. Prefix destinations remain managed by DokuWiki.

Overrides are stored as the template's `interwiki_styles` JSON setting and work without the companion plugin. One serialized value preserves changes across multiple prefixes without hitting PHP's form-variable limit. The server validates prefixes, field names, hex colors, and allowed style values before saving or generating CSS. CSS class names use DokuWiki's renderer normalization (for example `amazon.de` becomes `iw_amazon_de`). Both existing and dynamically loaded pane links receive the styles. This discovers configured prefixes rather than performing a full wiki content scan.

### Shared appearance values

Fokus's active screen styles use CSS variables supplied by the shared `settings-schema.php` defaults and saved template configuration. Palette fields show their real defaults. Empty color values resolve to those defaults. Accent backgrounds, text on accents, input colors, and generic interwiki links have dedicated controls; code/page-ID fonts and sidebar text size are configurable too.

Component color roles preserve existing neutral light/dark shades by default and inherit their source setting when that setting is customized. This covers pages, panes, sidebar, dialogs, editors, admin views, tables, media views, and links. Page Health and semantic integration-status colors retain their own styling. Print keeps its paper-oriented styles. Standard `style.ini` color replacements remain for DokuWiki/plugin compatibility; use Fokus Settings for Fokus appearance.

The template bundles pane/sidebar styles through DokuWiki's CSS pipeline. `appearance.php` emits validated variables and interwiki rules, rather than selector-specific color overrides. The generated `css/theme-defaults.css` supplies the same default variables for exports and before runtime overrides load. After changing schema defaults, regenerate it with `php lib/tpl/fokus/bin/build-appearance.php` from the wiki root. Configuration changes need no rebuild.
