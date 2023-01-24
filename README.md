# Nianteo
My collection of Vue3 components for a Nuxt3 use.  
Wip...  
(module creation the [Kaizen Codes](https://www.youtube.com/watch?v=5BcJ2WUTltU) way)

## `nianteo-list`
Generates a list from items.

### Props
`items: Array<unknown>` the items to list  
`nick?: string` the nick prop defines the name under which items and slot will be accessible. By default: `'item'`

### Usage


 ```typescript
const items = [
  {
    title: 'Title item 1',
    body: 'Body item 1'
  },
  {
    title: 'Title item 2',
    body: 'Body item 2'
  }
];
```


By default, each item is accessible in `item` slot, corresponding to the default nick `item` (see [Props](#props)).
```vue
<nianteo-list
  :items="items"
>
  <template #item="{ item, index }">
    <h2>{{ item.title }}</h2>
    <p>{{ item.body }}</p>
  </template>
</nianteo-list>
```


With custom `nick` prop:
```vue
<nianteo-list
  :items="items"
  nick="customNick"
>
  <template #customNick="{ customNick, index }">
    <h2>{{ customNick.title }}</h2>
    <p>{{ customNick.body }}</p>
  </template>
</nianteo-list>
```


### Other slots
`before` and `after` slots generate items at first and last place in list:
```vue
<nianteo-list
  :items="items"
  nick="customNick"
>
  <template #customNick="{ customNick, index }">
    <h2>{{ customNick.title }}</h2>
    <p>{{ customNick.body }}</p>
  </template>
  
  <template #before>
    <p>That's my before item</p>
  </template>
  
  <template #after>
    <p>That's my after item</p>
  </template>

</nianteo-list>
```
