# 📱 React Native - Easy Questions

> **Topics Covered:** What is React Native, React vs React Native Differences, Core Components (`View`, `Text`, `Image`, `TextInput`, `ScrollView`, `Button`, `Pressable`), Styling in React Native (`StyleSheet.create()`, Flexbox default column), Platform-specific file naming.

---

### Q1: What is React Native and How Does It Work?
**Question:** What is React Native? How does it differ from web React?

**Answer:**
- **React Native** is an open-source framework created by Meta that allows developers to build truly native mobile applications for iOS and Android using JavaScript and React.
- **Key Differences:**
  | Feature | React (Web) | React Native (Mobile) |
  | :--- | :--- | :--- |
  | **Rendering Target** | Web Browser DOM | Native iOS (UIKit) and Android (Android Views) |
  | **Core Elements** | `<div>`, `<span>`, `<p>`, `<img>` | `<View>`, `<Text>`, `<Image>`, `<TextInput>` |
  | **Styling** | CSS files, Tailwind, CSS-in-JS | `StyleSheet.create()` JavaScript objects |
  | **Flexbox Default** | `flexDirection: "row"` | `flexDirection: "column"` |
  | **Units** | `px`, `rem`, `em`, `vh`, `%` | Unitless numbers (Density-Independent Pixels DP) |
  | **Routing** | React Router, Next.js | React Navigation, Expo Router |

---

### Q2: Core React Native Components & Basic Layout
**Question:** What are the basic core components in React Native and how do you style them using `StyleSheet`?

**Answer:**
```jsx
import React from 'react';
import { View, Text, Image, StyleSheet, TextInput, Pressable } from 'react-native';

export default function UserCard() {
  return (
    <View style={styles.container}>
      <Image 
        source={{ uri: 'https://via.placeholder.com/100' }} 
        style={styles.avatar} 
      />
      <Text style={styles.title}>Utkarsh Singh</Text>
      <Text style={styles.subtitle}>Full Stack & Mobile Developer</Text>
      
      <TextInput 
        placeholder="Enter status..." 
        style={styles.input} 
      />
      
      <Pressable style={styles.button} onPress={() => alert('Saved!')}>
        <Text style={styles.buttonText}>Update Profile</Text>
      </Pressable>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    alignItems: 'center',
    justifyContent: 'center',
    backgroundColor: '#f8f9fa',
    padding: 20,
  },
  avatar: {
    width: 80,
    height: 80,
    borderRadius: 40,
    marginBottom: 12,
  },
  title: {
    fontSize: 20,
    fontWeight: 'bold',
    color: '#212529',
  },
  subtitle: {
    fontSize: 14,
    color: '#6c757d',
    marginBottom: 16,
  },
  input: {
    width: '100%',
    borderWidth: 1,
    borderColor: '#ced4da',
    borderRadius: 8,
    padding: 10,
    backgroundColor: '#fff',
    marginBottom: 12,
  },
  button: {
    backgroundColor: '#0066cc',
    paddingVertical: 12,
    paddingHorizontal: 24,
    borderRadius: 8,
  },
  buttonText: {
    color: '#ffffff',
    fontWeight: '600',
  },
});
```
---

### Q3: `FlatList` vs `map()` in React Native
**Question:** What is the difference between `FlatList` and `map()` when rendering lists in React Native?

**Answer:**
- **`map()`**: A standard JavaScript array method. Renders all list items at once in memory. Lacks native recycling, leading to high memory consumption and dropped frames for large datasets.
- **`FlatList`**: A specialized React Native list component built for performance. Uses **virtualization (windowing)** to render only items currently visible on the screen, recycling offscreen views.

```jsx
import { FlatList, Text, View } from 'react-native';

const users = [
  { id: '1', name: 'Utkarsh' },
  { id: '2', name: 'Rahul' },
];

// FlatList (Recommended for performance)
<FlatList
  data={users}
  keyExtractor={(item) => item.id}
  renderItem={({ item }) => (
    <View><Text>{item.name}</Text></View>
  )}
/>
```

---

### Q4: `ScrollView` vs `SafeAreaView`
**Question:** What is the difference between `ScrollView` and `SafeAreaView`?

**Answer:**
- **`ScrollView`**: A scrolling container that allows content larger than the device screen to be scrolled vertically or horizontally.
- **`SafeAreaView`**: A layout component that applies automatic padding to ensure content is rendered within the **safe boundaries of the device screen**, avoiding camera notches, home indicator bars, and rounded corners (primarily on iOS).

```jsx
import { SafeAreaView, ScrollView, Text, StyleSheet } from 'react-native';

export default function App() {
  return (
    <SafeAreaView style={styles.safeArea}>
      <ScrollView>
        <Text style={styles.text}>Safe Scrollable Content</Text>
      </ScrollView>
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  safeArea: { flex: 1, backgroundColor: '#ffffff' },
  text: { fontSize: 18, padding: 16 },
});
```
