```html
<ion-item href="#">
  <ion-label>Anchor Item</ion-label>
</ion-item>

<ion-item href="#" disabled="true">
  <ion-label>Disabled Anchor Item</ion-label>
</ion-item>

<ion-item button>
  <ion-label>Button Item</ion-label>
</ion-item>

<!--
  Note: The 'router-link' attribute requires a configured 
  routing library like Ionic's Web Component router for navigation to occur.
  Since this playground is a simplified snippet, 
  clicking these items will not trigger navigation.
-->
<ion-item router-link="#" router-direction="forward" onclick="alert('Navigating via JS!')">
  <ion-label>Router Link</ion-label>
</ion-item>
```
