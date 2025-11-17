# Expo HTK - Hacktoolkit for Expo

Complete utilities, services, components, and reusable design patterns for Expo/React Native applications.

## Table of Contents

- [Overview](#overview)
- [Quick Start](#quick-start)
- [Architecture](#architecture)
- [Documentation](#documentation)
- [Core Modules](#core-modules)
- [Technology Stack](#technology-stack)
- [Contributing](#contributing)
- [License](#license)

## Overview

Expo HTK is a comprehensive toolkit providing pre-built features, utilities, and components for accelerating Expo/React Native development. It includes:

- **Features**: Complete feature implementations (settings, themes, device info)
- **Components**: Reusable UI components (dialogs, forms, etc.)
- **Utilities**: Helper functions (string formatting, geo calculations, observers)
- **State**: Type-safe state management with automatic persistence
- **Theming**: Complete theme system with light/dark mode support
- **Storage**: Platform-aware storage (MMKV for mobile, localStorage for web)

## Quick Start

### Installation

This is a toolkit meant to be integrated into your Expo project. Copy or reference the modules you need.

### Basic Usage

#### 1. App Settings
```typescript
import { createAppSettings } from '@htk/features/appSettings';

const { useAppSettings, updateAppSetting } = createAppSettings({
 darkMode: false,
 fontSize: 16,
 language: 'en'
});

function MyComponent() {
 const settings = useAppSettings();
 const update = updateAppSetting();

 return (
 <View>
 <Toggle
 value={settings.darkMode}
 onValueChange={(val) => update('darkMode', val)}
 />
 </View>
 );
}
```

#### 2. Theme System
```typescript
import { createTheme } from '@htk/features/theme';

const { ThemeProvider, useThemeScheme, useChangeTheme } = createTheme({
 enabled: true,
 supportDarkMode: true,
 defaultScheme: 'light',
 schemes: {
 light: { /* colors */ },
 dark: { /* colors */ }
 }
});

function App() {
 return (
 <ThemeProvider>
 <MainApp />
 </ThemeProvider>
 );
}
```

#### 3. Dialog Components
```typescript
import { Confirm, useConfirm } from '@htk/components/Dialogs';

function App() {
 return (
 <Confirm>
 <MainApp />
 </Confirm>
 );
}

function MyComponent() {
 const { confirm } = useConfirm();

 return (
 <Button
 title="Delete"
 onPress={() => confirm({
 title: 'Confirm Delete?',
 buttons: [
 { label: 'Cancel', onPress: () => {} },
 { label: 'Delete', onPress: handleDelete }
 ]
 })}
 />
 );
}
```

## Architecture

```
expo-htk/
├── components/ # Reusable UI components
│ ├── Dialogs/ # Dialog components
│ └── README.md # Component guidelines
├── features/ # Complete feature modules
│ ├── appSettings/ # Settings management
│ ├── theme/ # Theme system
│ ├── expo/ # Expo integrations
│ └── README.md # Feature overview
├── states/ # State management
├── storages/ # Storage adapters
│ ├── mmkv/ # Mobile storage
│ └── localStorage/ # Web storage
├── types/ # TypeScript definitions
├── utils/ # Utility functions
│ ├── string/ # String utilities
│ ├── enum/ # Enum helpers
│ ├── observer/ # Observer pattern
│ ├── react/ # React utilities
│ ├── theme/ # Theme utilities
│ ├── geolocations.ts # Geographic calculations
│ ├── humanize.ts # Number formatting
│ ├── rollbar.ts # Error tracking
│ └── README.md # Utilities overview
├── constants.ts # Global constants
└── README.md # This file
```

## Documentation

Complete documentation for each module:

### Top-Level Documentation
- **[Components](components/README.md)** - UI component guidelines and Dialogs
- **[Features](features/README.md)** - Feature modules overview
- **[States](states/README.md)** - State management with Jotai
- **[Storages](storages/README.md)** - Storage adapters and persistence
- **[Types](types/README.md)** - Shared TypeScript definitions
- **[Utils](utils/README.md)** - Utility functions and helpers

### Feature Documentation
- **[App Settings](features/appSettings/README.md)** - Settings management system
 - [Components](features/appSettings/components/README.md)
 - [Entry Types](features/appSettings/components/Entries/README.md)
- **[Theme System](features/theme/README.md)** - Light/dark mode and theming
- **[Expo Features](features/expo/README.md)** - Expo-specific functionality
 - [Device Info](features/expo/deviceInfo/README.md)

### Component Documentation
- **[Dialogs](components/Dialogs/README.md)** - Dialog components
 - [Confirm Dialog](components/Dialogs/Confirm/README.md)

### Storage Documentation
- **[MMKV Storage](storages/mmkv/README.md)** - Mobile storage adapter
- **[LocalStorage](storages/localStorage/README.md)** - Web storage adapter

### Utility Documentation
- **[String Utils](utils/string/README.md)** - Text formatting
- **[Enum Utils](utils/enum/README.md)** - Enum helpers
- **[Observer Pattern](utils/observer/README.md)** - Event system
- **[React Utils](utils/react/README.md)** - Context builder
- **[Theme Utils](utils/theme/README.md)** - Styling helpers

## Core Modules

### Features

Complete, ready-to-use features combining components, state, and business logic:

#### App Settings
Type-safe settings management with UI and automatic persistence.

```typescript
import { createAppSettings } from '@htk/features/appSettings';

const { useAppSettings, updateAppSetting } = createAppSettings({
 isDarkMode: false,
 fontSize: 16
});
```

#### Theme System
Complete theme management with light/dark mode, system detection, and persistence.

```typescript
import { createTheme } from '@htk/features/theme';

const { ThemeProvider, useThemeScheme, useChangeTheme } = createTheme({
 enabled: true,
 supportDarkMode: true,
 schemes: { light: {...}, dark: {...} }
});
```

#### Expo Features
Device information and Expo-specific functionality.

```typescript
import { useDeviceInfo, ExpoDeviceInfo } from '@htk/features/expo/deviceInfo';

const device = useDeviceInfo();
<ExpoDeviceInfo /> // Display device info
```

### Components

Reusable, context-based UI components:

#### Confirm Dialog
Context-based confirmation dialog for user interactions.

```typescript
import { Confirm, useConfirm } from '@htk/components/Dialogs';

<Confirm>
 <App />
</Confirm>

const { confirm } = useConfirm();
```

### State Management

Jotai-based state management with automatic persistence:

```typescript
import { createPersistedState } from '@htk/states';

const persistedAtom = createPersistedState();
const userAtom = persistedAtom('user', defaultValue);
```

### Storage

Platform-aware storage adapters:

```typescript
import { storage } from '@htk/storages/mmkv'; // Mobile
// or
import { storage } from '@htk/storages/localStorage'; // Web

storage.setItem('key', JSON.stringify(value));
```

### Utilities

Helper functions for common tasks:

```typescript
import { capitalize, snakeCaseToCapitalize } from '@htk/utils/string';
import { enumToStr } from '@htk/utils/enum';
import { Observer } from '@htk/utils/observer';
import { contextBuilder } from '@htk/utils/react';
import { Dividers } from '@htk/utils/theme';
```

## Technology Stack

### Core
- **React Native** - Cross-platform UI framework
- **Expo** - React Native framework and services
- **TypeScript** - Type-safe JavaScript

### State & Storage
- **Jotai** - Primitive and flexible state management
- **react-native-mmkv** - High-performance mobile storage
- **localStorage** - Web storage API

### UI & Styling
- **react-native-ui-lib** - Comprehensive UI components and theming
- **@react-navigation/native** - Navigation integration

### Other
- **rollbar-react-native** - Error tracking
- **mapbox** - Geolocation and mapping
- **humanize-plus** - Number formatting

## Dependencies

### Required
- `react-native` - Core framework
- `expo` - Platform and services
- `react-native-ui-lib` - UI library
- `jotai` - State management

### Optional (by feature)
- `react-native-mmkv` - Mobile storage
- `@react-navigation/native` - Navigation
- `rollbar-react-native` - Error tracking
- `axios` - HTTP client

## Usage Examples

### Settings Screen
```typescript
import { AppSettings } from '@htk/features/appSettings/components';

function SettingsScreen() {
 const entries = [
 { type: 'switch', key: 'darkMode', label: 'Dark Mode' },
 { type: 'fontFamily', key: 'fontFamily', label: 'Font' },
 { type: 'fontSize', key: 'fontSize', label: 'Size' }
 ];

 return <AppSettings entries={entries} onSettingChange={handleChange} />;
}
```

### Themed Component
```typescript
import { useThemeScheme } from '@htk/features/theme';

function ThemedCard() {
 const scheme = useThemeScheme();

 return (
 <View style={{
 backgroundColor: scheme === 'dark' ? '#000' : '#fff'
 }}>
 <Text>Theme-aware content</Text>
 </View>
 );
}
```

### Observer Pattern
```typescript
import { Observer } from '@htk/utils/observer';

const observer = new Observer<UserData, 'updated' 'deleted'>();

observer.subscribe('updated', (data) => {
 console.log('User updated:', data);
});

observer.notify('updated', userData);
```

## Testing

Components and utilities are designed to be testable:

```typescript
import { render } from '@testing-library/react-native';
import { Confirm, useConfirm } from '@htk/components/Dialogs';

test('confirm dialog works', () => {
 const { getByText } = render(
 <Confirm>
 <ConfirmButton />
 </Confirm>
 );

 fireEvent.press(getByText('Confirm'));
});
```

## Best Practices

### Do
- Use type-safe state management
- Leverage automatic persistence
- Follow component guidelines
- Integrate with theme system
- Document custom extensions
- Test thoroughly

### Don't
- Hard-code colors or spacing
- Mix multiple state systems
- Store sensitive data unencrypted
- Skip TypeScript types
- Ignore accessibility
- Forget error handling

## Getting Started

1. **Review Architecture** - Understand the folder structure and module organization
2. **Read Feature Docs** - Choose features relevant to your app
3. **Set Up Features** - Initialize and configure needed features
4. **Use Components** - Integrate pre-built components
5. **Extend as Needed** - Create custom components following guidelines

## Contributing

When adding new features or components:

1. Follow the established patterns and conventions
2. Provide comprehensive documentation
3. Include usage examples
4. Write tests
5. Ensure TypeScript support
6. Support theming and customization

See individual module documentation for specific guidelines:
- [Component Guidelines](components/README.md#development-guidelines)
- [Feature Patterns](features/README.md#feature-development-pattern)
- [Utility Organization](utils/README.md)

## License

MIT License - Copyright 2024 Hacktoolkit

See LICENSE file for details.

## Related Resources

- [Expo Documentation](https://docs.expo.dev)
- [React Native Docs](https://reactnative.dev)
- [Jotai](https://jotai.org)
- [react-native-ui-lib](https://wix.github.io/react-native-ui-lib/)
- [TypeScript Handbook](https://www.typescriptlang.org/docs/)

## Tips

- **Type Safety**: Always use TypeScript for better development experience
- **Persistence**: App settings and theme preferences are automatically persisted
- **Theming**: All components respect the theme system - light/dark modes update automatically
- **Performance**: Use memoization for expensive computations in settings/theme hooks
- **Storage**: Choose MMKV for mobile (faster), localStorage for web

## Troubleshooting

For issues with specific modules:
- **Components**: See [Component Documentation](components/README.md)
- **State**: See [State Management](states/README.md)
- **Storage**: See [Storage Documentation](storages/README.md)
- **Features**: See specific feature README files
- **Utils**: See [Utils Documentation](utils/README.md)

---

**Last Updated**: 2024
**Version**: 1.0.0
