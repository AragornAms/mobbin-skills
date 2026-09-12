# Native controls — use the platform's and wire them correctly

A native-feeling app is largely assembled from controls the operating system
already ships. Rebuild a control only when the product truly diverges, then
match the platform's behavior, timing, accessibility, and haptics.

## Control selection

| Need | iOS | Android | Common React Native choice |
|---|---|---|---|
| Toggle | Switch | Material Switch | `Switch` from `react-native` |
| Single choice, two to five options | Segmented control | Tabs or segmented buttons | `@react-native-segmented-control/segmented-control` when appropriate |
| Value in a range | Slider | Material Slider | `@react-native-community/slider` |
| Date or time | Wheel or inline calendar | Material picker | `@react-native-community/datetimepicker` |
| Item actions | Context menu | Popup menu | A native-menu wrapper such as `zeego` |
| Destructive confirmation | Action sheet | Bottom sheet or dialog | Platform action-sheet/dialog abstraction |
| Bottom-sheet content | Detented sheet | Bottom sheet | `@gorhom/bottom-sheet` where it fits the project |
| Search | Navigation-integrated search | SearchView | Expo Router `headerSearchBarOptions` when supported |
| Pull to refresh | UIRefreshControl | SwipeRefreshLayout | `RefreshControl` |
| Haptics | Native feedback generator | Platform vibration/haptics | `expo-haptics` |
| In-app browser | SFSafariViewController | Custom Tabs | `expo-web-browser` |

Verify package availability and current APIs in the project before adding a
dependency. Preserve an existing design-system wrapper when it already exposes
the correct native behavior.

## Menus

Put item-level actions such as rename, share, archive, and delete in a native
context or popup menu anchored to the item. Match platform ordering and icons.
Mark destructive actions with the native destructive role and require a
confirmation step when the action cannot be easily undone. Never hide a bare,
irreversible delete behind one accidental tap.

## Bottom sheets

- Use content-derived detents or recognizable platform stops rather than
  arbitrary percentages.
- Use the sheet library's scroll-aware list or scroll container so drag and
  inner scrolling hand off correctly.
- Tie backdrop opacity to the sheet position. Support tap-to-dismiss only when
  dismissal is safe.
- Test keyboard appearance and dismissal with every editable field focused.
- A multi-step task belongs in a modal stack. Do not keep adding navigation to
  what began as a small sheet.

## Forms and inputs

- Keep persistent labels visible; do not use placeholder text as the only label.
- Set `keyboardType`, `autoComplete`, and `textContentType` deliberately. Use
  the one-time-code content type for OTP fields.
- Chain Return keys through fields and let the final field submit when safe.
- Validate at a useful boundary such as blur or submit. Do not flash errors on
  every keystroke unless immediate validation genuinely helps.
- Put a specific error beside the field and keep it visible until resolved.
- Use a keyboard-avoiding strategy that tracks the native keyboard and has been
  tested on both appearance and dismissal.

## Navigation patterns

- Use stacks for drill-in, tabs for top-level peers, modals for self-contained
  tasks, and sheets for short interruptions.
- Preserve the iOS interactive-pop gesture unless Back is blocked for a valid
  unsaved-work or irreversible-request reason.
- Keep tab bars recognizable: normally three to five items, persistent labels,
  and coherent active/inactive icon variants.
- Make addressable screens real routes so deep links can build a valid stack.

## When rebuilding a control

Observe the native control first, ideally alongside relevant Mobbin references.
Match its geometry, pressed and disabled states, timing, gesture thresholds,
haptics, accessibility semantics, and focus behavior. Test on actual iOS and
Android builds; do not assume one platform's imitation is correct on the other.
