

## Fix Task Column to Actually Respect 70% Width

The Task column header is already set to `70%` in the code, but the browser is ignoring it because the HTML table uses `auto` layout by default. The browser recalculates column widths based on content, overriding the specified percentages.

### Root Cause
The `<Table>` component doesn't have `table-layout: fixed`, so percentage widths are treated as suggestions rather than enforced values.

### Fix
**File: `src/components/DealExpandedPanel.tsx`** (line ~785)

Add `table-layout: fixed` and `width: 100%` to the Action Items `<Table>` element:

```tsx
<Table className="table-fixed w-full">
```

This single change forces the browser to strictly respect the percentage widths already defined:
- `#`: 3%
- **Task**: 70%  
- **Assigned To**: 8%
- **Due**: 8%
- **Status**: 4%
- **Priority**: 4%
- **Actions**: 3%

No other changes needed -- the percentages are already correctly set.

