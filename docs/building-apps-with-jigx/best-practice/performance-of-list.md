# Performance of List

## Difference between `jig.list` and `component.list`

Understanding when to use [jig.list](https://docs.jigx.com/examples/readme/jig-types/jig_list) versus [component.list](https://docs.jigx.com/examples/readme/components/list) is essential for building performant Jigx applications.

### Use `jig.list` for large datasets

Use `jig.list` when you have hundreds or thousands of items. This component only renders items currently visible on screen, making it ideal for large datasets. Because it occupies the full screen, you cannot place other components above or below it. This constraint is necessary to maintain optimal performance.

Always use Jigx's built-in list item components, such as `component.list-item` or `component.product-item`, with `jig.list`. These components are specifically optimized for both iOS and Android. Avoid using `component.custom-component` as list items, as custom components require significantly more resources and will impact performance, especially on Android.

### Use `component.list` for small previews

Use `component.list` when displaying up to twenty items as previews, showing multiple lists on one screen, or when you need to place other components above or below the list. This is perfect for dashboard-style layouts with quick overviews.

Never display more than twenty items in `component.list`. Exceeding this limit, you'll experience significant performance issues, particularly on Android. For larger datasets, display a preview with a "_Show more_" button that navigates to a dedicated `jig.list` screen.

Unlike `jig.list`, you can use `component.custom-component` with `component.list`, but only when displaying a handful of items.

### Making the right choice

* Choose `jig.list` when you have hundreds or thousands of items, need search and filter capabilities, or can dedicate a full screen to browsing.&#x20;
* Choose `component.list` when you have twenty items or fewer, need multiple lists on one screen, or want to show previews alongside other content.
* Don't use `component.list` with 100+ items just because you want components above or below the list. Think about alternative UI designs that better serve your users.

## Effect of `hasDynamicHeight` property

By default, Jigx calculates the list item height once, based on your YAML configuration and applies it to all items. This means every item has the same height, which provides optimal performance but also reserves space for optional content even when it isn't present.

For example, if your configuration includes tags but only one out of ten items has tags, all items will still reserve space for tags, creating empty gaps in items without tags.

### When to use `hasDynamicHeight`

The `hasDynamicHeight` option calculates the height of each item based on its actual content, allowing items to have different heights. This removes wasted space but requires more processing.

Use `hasDynamicHeight` when:

* You have approximately fifty items or fewer.
* Content varies significantly between items.
* The UI improvement outweighs the performance cost.&#x20;

The acceptable number depends on UI complexity: simple items might handle a hundred items well, while complex items with images and nested components may show issues around thirty items.

Use fixed height (default) when:

* You have hundreds or thousands of items.
* &#x20;Performance is critical.
* Item content is relatively consistent.

### Testing is essential

Always test your lists with `hasDynamicHeight` both enabled and disabled. Scroll through the list on actual devices, especially Android, and evaluate scroll smoothness, initial load time, and overall responsiveness. Choose the configuration that delivers the best balance for your specific use case.

The `hasDynamicHeight` option applies to both `jig.list` and `component.list`, since it’s configured on `component.list-item`. However, remember that `jig.list` is designed for large datasets where using dynamic height may cause significant performance issues.

## Custom Components in Lists

[Custom components](../ui/custom-components-_alpha_/custom-components-_alpha_.md) let you build UI from low-level components such as [view](../ui/custom-components-_alpha_/inputs-_-outputs-_alpha_.md), [button](../ui/custom-components-_alpha_/inputs-_-outputs-_alpha_.md), and [text](../ui/custom-components-_alpha_/inputs-_-outputs-_alpha_.md). While this provides flexibility, list items need special optimization for scrolling and rendering that built-in components provide.

### Never in `jig.list`, cautiously in `component.list`

Never use `component.custom-component` as items in `jig.list`. This will cause laggy scrolling, increased memory usage, and poor rendering performance, especially on Android.

You can use custom components in `component.list`, but only when displaying ten items or fewer. Always test thoroughly on actual devices, monitor scrolling smoothness and rendering speed, particularly on Android.

### Why built-in components matter

Built-in list item components like `component.list-item` and `component.product-item` are designed specifically for list rendering. They are optimized for the native OS level to:

* &#x20;Calculate heights efficiently.
* Recycle components during scrolling.
* Manage memory for large datasets.&#x20;

Custom components lack these optimizations, making them less suitable for lists with frequent updates or large numbers of items.

If you need custom components in a list and experience performance issues during testing, switch to built-in components instead. Reserve custom components for non-list UI elements where list-specific performance requirements are not required.

## Swipeable Actions

Swipeable actions allow users to swipe list items to reveal action buttons. However, lists that include swipeable actions currently render up to 30% slower compared to lists without them, with the performance impact most noticeable on Android. The Jigx team is actively working on optimizations to improve performance in future releases.

### Performance alternatives

If swipeable actions cause performance issues, consider these alternatives:

* **Action buttons in list items** - Display action icons directly in each item. These are always visible with no additional performance overhead.
* **Detail screen actions** - Let users tap a list item to navigate to a detail screen where the relevant actions are available. This keeps the main list simple and highly performant.

Start by building your list **without** swipeable actions and test the basic performance. Then add swipeable actions only if needed and test again. If rendering time increases significantly, use one of the alternative approaches above.

***

By following these performance best practices, you'll create Jigx applications that are both beautiful and fast. Remember, performance optimization is about finding the right balance for your specific use case, test on real devices, measure the results, and choose the approach that delivers the best experience for your users.
