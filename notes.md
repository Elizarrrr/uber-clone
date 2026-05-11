1.  index.tsx
    import { Image } from 'expo-image';
    import { Platform, StyleSheet } from 'react-native';

    import { HelloWave } from '@/components/hello-wave';
    import ParallaxScrollView from '@/components/parallax-scroll-view';
    import { ThemedText } from '@/components/themed-text';
    import { ThemedView } from '@/components/themed-view';
    import { Link } from 'expo-router';

    export default function HomeScreen() {
    return (
        <ParallaxScrollView
        headerBackgroundColor={{ light: '#A1CEDC', dark: '#1D3D47' }}
        headerImage={
            <Image
            source={require('@/assets/images/partial-react-logo.png')}
            style={styles.reactLogo}
            />
        }>
        <ThemedView style={styles.titleContainer}>
            <ThemedText type="title">Welcome!</ThemedText>
            <HelloWave />
        </ThemedView>
        <ThemedView style={styles.stepContainer}>
            <ThemedText type="subtitle">Step 1: Try it</ThemedText>
            <ThemedText>
            Edit <ThemedText type="defaultSemiBold">app/(tabs)/index.tsx</ThemedText> to see changes.
            Press{' '}
            <ThemedText type="defaultSemiBold">
                {Platform.select({
                ios: 'cmd + d',
                android: 'cmd + m',
                web: 'F12',
                })}
            </ThemedText>{' '}
            to open developer tools.
            </ThemedText>
        </ThemedView>
        <ThemedView style={styles.stepContainer}>
            <Link href="/modal">
            <Link.Trigger>
                <ThemedText type="subtitle">Step 2: Explore</ThemedText>
            </Link.Trigger>
            <Link.Preview />
            <Link.Menu>
                <Link.MenuAction title="Action" icon="cube" onPress={() => alert('Action pressed')} />
                <Link.MenuAction
                title="Share"
                icon="square.and.arrow.up"
                onPress={() => alert('Share pressed')}
                />
                <Link.Menu title="More" icon="ellipsis">
                <Link.MenuAction
                    title="Delete"
                    icon="trash"
                    destructive
                    onPress={() => alert('Delete pressed')}
                />
                </Link.Menu>
            </Link.Menu>
            </Link>

            <ThemedText>
            {`Tap the Explore tab to learn more about what's included in this starter app.`}
            </ThemedText>
        </ThemedView>
        <ThemedView style={styles.stepContainer}>
            <ThemedText type="subtitle">Step 3: Get a fresh start</ThemedText>
            <ThemedText>
            {`When you're ready, run `}
            <ThemedText type="defaultSemiBold">npm run reset-project</ThemedText> to get a fresh{' '}
            <ThemedText type="defaultSemiBold">app</ThemedText> directory. This will move the current{' '}
            <ThemedText type="defaultSemiBold">app</ThemedText> to{' '}
            <ThemedText type="defaultSemiBold">app-example</ThemedText>.
            </ThemedText>
        </ThemedView>
        </ParallaxScrollView>
    );
    }

    const styles = StyleSheet.create({
    titleContainer: {
        flexDirection: 'row',
        alignItems: 'center',
        gap: 8,
    },
    stepContainer: {
        gap: 8,
        marginBottom: 8,
    },
    reactLogo: {
        height: 178,
        width: 290,
        bottom: 0,
        left: 0,
        position: 'absolute',
    },
    });

2.  _layout.tsx
    import "../global.css";
    import { DarkTheme, DefaultTheme, ThemeProvider } from '@react-navigation/native';
    import { Stack } from 'expo-router';
    import { StatusBar } from 'expo-status-bar';
    import 'react-native-reanimated';

    import { useColorScheme } from '@/hooks/use-color-scheme';

    export const unstable_settings = {
    anchor: '(tabs)',
    };

    export default function RootLayout() {
    const colorScheme = useColorScheme();

    return (
        <ThemeProvider value={colorScheme === 'dark' ? DarkTheme : DefaultTheme}>
        <Stack>
            <Stack.Screen name="(tabs)" options={{ headerShown: false }} />
            <Stack.Screen name="modal" options={{ presentation: 'modal', title: 'Modal' }} />
        </Stack>
        <StatusBar style="auto" />
        </ThemeProvider>
    );
    }

3.  modal.tsx
    C:\Users\joyli\Downloads\VS Code Projects\uber-clone\app\modal.tsx

    import { Link } from 'expo-router';
    import { StyleSheet } from 'react-native';

    import { ThemedText } from '@/components/themed-text';
    import { ThemedView } from '@/components/themed-view';

    export default function ModalScreen() {
    return (
        <ThemedView style={styles.container}>
        <ThemedText type="title">This is a modal</ThemedText>
        <Link href="/" dismissTo style={styles.link}>
            <ThemedText type="link">Go to home screen</ThemedText>
        </Link>
        </ThemedView>
    );
    }

    const styles = StyleSheet.create({
    container: {
        flex: 1,
        alignItems: 'center',
        justifyContent: 'center',
        padding: 20,
    },
    link: {
        marginTop: 15,
        paddingVertical: 15,
    },
    });

4.  app.json
    {
    "expo": {
        "name": "uber-clone",
        "slug": "uber-clone",
        "version": "1.0.0",
        "orientation": "portrait",
        "icon": "./assets/images/icon.png",
        "scheme": "uberclone",
        "userInterfaceStyle": "automatic",
        "newArchEnabled": true,
        "ios": {
        "supportsTablet": true
        },
        "android": {
        "adaptiveIcon": {
            "backgroundColor": "#E6F4FE",
            "foregroundImage": "./assets/images/android-icon-foreground.png",
            "backgroundImage": "./assets/images/android-icon-background.png",
            "monochromeImage": "./assets/images/android-icon-monochrome.png"
        },
        "edgeToEdgeEnabled": true,
        "predictiveBackGestureEnabled": false
        },
        "web": {
        "output": "static",
        "favicon": "./assets/images/favicon.png"
        },
        "plugins": [
        "expo-router",
        [
            "expo-splash-screen",
            {
            "image": "./assets/images/splash-icon.png",
            "imageWidth": 200,
            "resizeMode": "contain",
            "backgroundColor": "#ffffff",
            "dark": {
                "backgroundColor": "#000000"
            }
            }
        ]
        ],
        "experiments": {
        "typedRoutes": true,
        "reactCompiler": true
        }
    }
    }

5.  _layout.tsx

    import { useFonts } from "expo-font";
    import { Stack } from "expo-router";
    import "react-native-reanimated";
    import "../global.css";

    export const unstable_settings = {
    anchor: "(tabs)",
    };

    export default function RootLayout() {
    const [loaded] = useFonts({
        "Jakarta-Bold": require("../assets/fonts/PlusJakartaSans-Bold.ttf"),
        "Jakarta-ExtraBold": require("../assets/fonts/PlusJakartaSans-ExtraBold.ttf"),
        "Jakarta-ExtraLight": require("../assets/fonts/PlusJakartaSans-ExtraLight.ttf"),
        "Jakarta-Light": require("../assets/fonts/PlusJakartaSans-Light.ttf"),
        "Jakarta-Medium": require("../assets/fonts/PlusJakartaSans-Medium.ttf"),
        "Jakarta-Regular": require("../assets/fonts/PlusJakartaSans-Regular.ttf"),
        "Jakarta-SemiBold": require("../assets/fonts/PlusJakartaSans-SemiBold.ttf"),
    });

    return (
        <Stack>
        <Stack.Screen name="index" options={{ headerShown: false }} />
        <Stack.Screen name="+not-found" />
        </Stack>
    );
    }

6.  structure of components

    const ComponentName = () => ();

    export default ComponentName;

7.  C:\Users\joyli\Downloads\VS Code Projects\uber-clone\lib\auth.ts
    export interface TokenCache {
    getToken: (key: string) => Promise<string | undefined | null>;
    saveToken: (key: string, token: string) => Promise<void>;
    clearToken: (key: string) => void;
    }

    export const tokenCache: TokenCache = {
        async getToken(key: string) {
            try {
            return SecureStore.getItemAsync(key);
            } catch (err) {
            return null;
            }
        },
        async saveToken(key: string, value: string) {
            try {
            return SecureStore.setItemAsync(key, value);
            } catch (err) {
            return;
            }
        },
        clearToken(key: string) {
            SecureStore.deleteItemAsync(key);
        },
    };

8.  C:\Users\joyli\Downloads\VS Code Projects\uber-clone\app\(root)\(tabs)\home.tsx
    import { Show, useUser } from '@clerk/expo'
    import { useClerk } from '@clerk/expo'
    import { Link } from 'expo-router'
    import { Text, View, Pressable, StyleSheet } from 'react-native'

    export default function Page() {
    const { user } = useUser()
    const { signOut } = useClerk()

    return (
        <View style={styles.container}>
        <Text style={styles.title}>Welcome!</Text>
        <Show when="signed-out">
            <Link href="/(auth)/sign-in">
            <Text>Sign in</Text>
            </Link>
            <Link href="/(auth)/sign-up">
            <Text>Sign up</Text>
            </Link>
        </Show>
        <Show when="signed-in">
            <Text>Hello {user?.emailAddresses[0].emailAddress}</Text>
            <Pressable style={styles.button} onPress={() => signOut()}>
            <Text style={styles.buttonText}>Sign out</Text>
            </Pressable>
        </Show>
        </View>
    )
    }

9.  C:\Users\joyli\Downloads\VS Code Projects\uber-clone\app\(auth)\sign-up.tsx
    const handleSubmit = async () => {
        const { error } = await signUp.password({
        emailAddress,
        password,
        })
        if (error) {
        console.error(JSON.stringify(error, null, 2))
        return
        }

        if (!error) await signUp.verifications.sendEmailCode()
    }

    const handleVerify = async () => {
        await signUp.verifications.verifyEmailCode({
        code,
        })
        if (signUp.status === 'complete') {
        await signUp.finalize({
            // Redirect the user to the home page after signing up
            navigate: ({ session, decorateUrl }) => {
            if (session?.currentTask) {
                // Handle pending session tasks
                // See https://clerk.com/docs/guides/development/custom-flows/authentication/session-tasks
                console.log(session?.currentTask)
                return
            }

            const url = decorateUrl('/')
            if (url.startsWith('http')) {
                window.location.href = url
            } else {
                router.push(url as Href)
            }
            },
        })
        } else {
        // Check why the sign-up is not complete
        console.error('Sign-up attempt not complete:', signUp)
        }
    }

    if (signUp.status === 'complete' || isSignedIn) {
        return null
    }

    if (
        signUp.status === 'missing_requirements' &&
        signUp.unverifiedFields.includes('email_address') &&
        signUp.missingFields.length === 0
    ) 

10. vercel.json
    {
    "rewrites": [
        {
        "source": "/(.*)",
        "destination": "/"
        }
    ]
    }

