---
description: Display collection items in your component templates
---

# Accessing Data in Templates

Collection data is automatically available in your templates through the `collections` object. Each collection is accessible by its property name as defined in your component's `properties.json`.

## Syntax

Access a collection using `collections.{property-name}`:

```html
@each(item in collections.features)
    <div>{{item.title}}</div>
@endeach
```

## Basic Example

Given a `features` collection with `title` and `description` properties:

```html
<ul class="features-list">
    @each(feature in collections.features)
        <li>
            <h3>{{feature.title}}</h3>
            <p>{{feature.description}}</p>
        </li>
    @endeach
</ul>
```

## Real-World Examples

### Audio Playlist Tracks

The Audio Playlist component iterates over tracks to build a playlist:

```html
<ul class="{{classes.list}}">
    @each(track in tracks)
        <li
            data-track
            data-title="{{track.title}}"
            data-artist="{{track.artist}}"
            data-cover="{{track.coverImage}}"
            data-url="{{track.audioSource.path}}"
            class="{{classes.track.wrapper}}"
        >
            <img
                src="{{track.coverImage}}"
                class="{{classes.track.artwork}}"
                alt="cover"
            />
            <div class="flex-1">
                <h4 class="{{classes.track.title}}">{{track.title}}</h4>
                <p class="{{classes.track.artist}}">{{track.artist}}</p>
            </div>
            <div
                x-cloak
                class="[&_svg]:size-4"
                x-show="currentTrackIndex === {{track::index}}"
                @click.stop="togglePlay"
            >
                <template x-if="!isPlaying">{{iconPlay}}</template>
                <template x-if="isPlaying">{{iconPause}}</template>
            </div>
        </li>
    @endeach
</ul>
```

Note: In this example, `tracks` is passed from hooks.js after being extracted from `rw.collections.tracks`.

### Feature Cards with Icons

Display a grid of feature cards:

```html
<div class="grid grid-cols-3 gap-6">
    @each(feature in collections.features)
        <div class="feature-card">
            @if(feature.icon)
                <img src="{{feature.icon}}" alt="" class="feature-icon" />
            @endif
            <h3>{{feature.title}}</h3>
            <p>{{feature.description}}</p>
        </div>
    @endeach
</div>
```

### Pricing Tiers

Create a pricing table from collection data:

```html
<div class="pricing-grid">
    @each(tier in collections.tiers)
        <div class="pricing-card @if(tier.featured) pricing-featured @endif">
            <h3>{{tier.name}}</h3>
            <div class="price">
                <span class="amount">{{tier.price}}</span>
                <span class="period">{{tier.period}}</span>
            </div>
            <p class="description">{{tier.description}}</p>
            <a href="{{tier.link.href}}" class="cta-button">
                {{tier.buttonText}}
            </a>
        </div>
    @endeach
</div>
```

### Team Members

Display team member profiles:

```html
<div class="team-grid">
    @each(member in collections.team)
        <div class="team-member">
            <img src="{{member.photo}}" alt="{{member.name}}" />
            <h4>{{member.name}}</h4>
            <p class="role">{{member.role}}</p>
            <p class="bio">{{member.bio}}</p>
        </div>
    @endeach
</div>
```

## Using Loop Variables

Within collection loops, you have access to special loop variables:

| Variable | Description |
|----------|-------------|
| `::index` | Zero-based index of the current item |
| `::isFirst` | True if this is the first item |
| `::isLast` | True if this is the last item |

### Example with Loop Variables

```html
@each(slide in collections.slides)
    <div 
        class="slide @if(slide::isFirst) slide-active @endif"
        data-index="{{slide::index}}"
    >
        <img src="{{slide.image}}" alt="{{slide.caption}}" />
    </div>
@endeach
```

### First/Last Styling

```html
<ul class="breadcrumbs">
    @each(item in collections.items)
        <li class="@if(item::isLast) current @endif">
            @if(!item::isLast)
                <a href="{{item.link}}">{{item.title}}</a>
                <span class="separator">/</span>
            @else
                <span>{{item.title}}</span>
            @endif
        </li>
    @endeach
</ul>
```

## Handling Empty Collections

Check if a collection has items before rendering:

```html
@if(hasFeatures)
    <div class="features">
        @each(feature in collections.features)
            <div class="feature">{{feature.title}}</div>
        @endeach
    </div>
@else
    <p class="empty-state">No features have been added yet.</p>
@endif
```

The `hasFeatures` boolean is typically computed in your hooks.js file. See [Data Collections in hooks.js](data-collections-in-hooks.js.md) for details.

## Accessing Nested Properties

Collection items can have complex nested data:

```html
@each(item in collections.items)
    <!-- Simple property -->
    <h3>{{item.title}}</h3>
    
    <!-- Resource property -->
    <img src="{{item.image}}" alt="{{item.title}}" />
    
    <!-- Link property -->
    <a href="{{item.link.href}}" target="{{item.link.target}}">
        {{item.link.title}}
    </a>
    
    <!-- Resource with path -->
    <audio src="{{item.audioFile.path}}"></audio>
@endeach
```

## Best Practices

1. **Use meaningful loop variable names** - Choose names that describe the item: `feature`, `track`, `member`, not generic names like `item` or `i`.

2. **Handle empty states** - Always consider what happens when a collection is empty.

3. **Use hooks.js for preprocessing** - If you need to transform collection data, do it in hooks.js rather than complex template logic.

4. **Access via passed props when needed** - For complex components, pass collections from hooks.js to templates as props for cleaner code.

## Related

- [@each](../language/each.md) - Loop directive reference
- [Data Collections in hooks.js](data-collections-in-hooks.js.md) - Processing collections in JavaScript
