# components/stuff Library

#### Filterable list of things
- filter is based on Topics
- filter can be set via url (controller action)
- items in list can be opened (read more)
- items in list can be accessed (read more, scroll into view) via url (controller action)

[Dr. Platz Services Block](https://bitbucket.org/externelemonbrain/drplatz_comp/src/main/public/packages/drplatz/blocks/services/)


#### PageAnchor to scroll/jump to
- has single text input for anchor string
- converts string to url safe
- displays converted string to logged-in users for copying

[nimbus Anchor Block](https://bitbucket.org/externelemonbrain/nimbus_comp/src/main/public/packages/nimbus/blocks/page_anchor/)


## css stuff

#### suprfluid breakpoint stepper

```scss
@function fluid-value($min-width, $max-width, $min-value, $max-value) {
    $slope: ($max-value - $min-value) / ($max-width - $min-width);
    $base: $min-value - ($slope * $min-width);

    @return clamp(
        #{$min-value}px,
        #{$base}px + #{$slope * 100}vw,
        #{$max-value}px
    );
}

@mixin responsive-fluid($property, $breakpoints, $values) {
    @if length($breakpoints) != length($values) {
        @error "Breakpoint and value lists must be of equal length.";
    }

    // Initial value before the first breakpoint
    $initial-value: nth($values, 1);
    #{$property}: #{$initial-value}px;

    // Loop through each breakpoint range
    @for $i from 2 through length($breakpoints) {
        $min-width: nth($breakpoints, $i - 1);
        $max-width: nth($breakpoints, $i);
        $min-value: nth($values, $i - 1);
        $max-value: nth($values, $i);

        @media (min-width: #{$min-width}px) {
            #{$property}: fluid-value($min-width, $max-width, $min-value, $max-value);
        }
    }

    // Final hard stop after last breakpoint
    $last-breakpoint: nth($breakpoints, -1);
    $last-value: nth($values, -1);

    @media (min-width: #{$last-breakpoint}px) {
        #{$property}: #{$last-value}px;
    }
}
```
usage:
```scss
h1 {
    @include f.responsive-fluid('font-size', (900, 1200, 1400, 1920), (28, 40, 48, 60));
    @include f.responsive-fluid('line-height', (900, 1200, 1400, 1920), (38, 48, 54, 68));
}
```
