# Plugins

Relevant official examples:
[`plugin`](https://github.com/bevyengine/bevy/blob/latest/examples/app/plugin.rs),
[`plugin_group`](https://github.com/bevyengine/bevy/blob/latest/examples/app/plugin_group.rs).

---

As your project grows, it can be useful to make it more modular. You can
split it into plugins.

Plugins are simply collections of things to be added to the
[App Builder](./app-builder.md).

```rust,no_run,noplayground
{{#include ../code/src/basics.rs:plugins}}
```

For internal organization in your own project, the main value of plugins
comes from not having to declare all your Rust types and functions as
`pub`, just so they can be accessible from `main` to be added to the app
builder. Plugins let you add things to your app from multiple different
places, like separate Rust files / modules.

You can decide how plugins fit into the architecture of your game.

Some suggestions:
 - Create plugins for different [states](./states.md).
 - Create plugins for various sub-systems, like physics or input handling.

## Plugin groups

Plugin groups register multiple plugins at once. Bevy's `DefaultPlugins`
and `MinimalPlugins` are examples of this. To create your own plugin group:

```rust,no_run,noplayground
{{#include ../code/src/basics.rs:plugin-groups}}
```

When adding a plugin group, you can disable some plugins while keeping
the rest.

For example, if you want to manually set up logging (with your own `tracing`
subscriber), you can disable `LogPlugin`:

```rust,no_run,noplayground
{{#include ../code/src/basics.rs:plugin-groups-disable}}
```

Note that this simply disables the functionality, but it cannot actually
remove the code to avoid binary bloat. The disabled plugins still have to
be compiled into your program.

If you want to slim down your build, you should look at disabling Bevy's
default cargo features, or depending on the various Bevy sub-crates
individually.

## Publishing Crates

Plugins give you a nice way to publish Bevy-based libraries for other people
to easily include into their projects.

If you intend to publish plugins as crates for public use, you should read
[the official guidelines for plugin authors](https://github.com/bevyengine/bevy/blob/main/docs/plugins_guidelines.md).

Don't forget to submit an entry to [Bevy Assets](https://bevyengine.org/assets)
on the official website, so that people can find your plugin
more easily. You can do this by making a PR in [the Github
repo](https://github.com/bevyengine/bevy-assets).

If you are interested in supporting bleeding-edge Bevy (main), [see here
for advice](../setup/bevy-git.md#advice-for-plugin-authors).
