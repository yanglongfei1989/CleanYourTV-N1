# N1 Remote integration notes

## Provider contract

Authority:

```text
com.gathin.n1remote.status
```

URI:

```text
content://com.gathin.n1remote.status/status
```

Columns:

- `ip`
- `port`
- `pin`
- `serviceOnline`
- `url`

The launcher queries only when Home is visible. The card is non-focusable and does not participate
in D-pad navigation.

## Startup layout

N1 package discovery can finish after the first Window focus. The launcher therefore:

1. Reconciles the Dock padding at several startup checkpoints.
2. Waits for the first child view to exist.
3. Clears transient focus from the empty RecyclerView.
4. Focuses the first dock card and only then clears the cold-start flag.
5. Refits the shared highlight after the Dock layout settles.

## Icon banners

`app_banners` maps package names to bundled drawable names:

```xml
<item>com.gathin.n1remote=banner_n1remote</item>
<item>com.github.avbox.osc=banner_avbox</item>
<item>com.android.tv.settings=banner_settings</item>
```

This survives an app update or reinstall as long as the package name is unchanged.

