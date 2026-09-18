<script lang="ts">
    import { page } from '$app/state';
    import { onMount } from 'svelte';

    let username = $derived(page.params.id);
    let user = $state(null);
    let loading = $state(false);
    let error = $state(null);

    async function getData(username) {
        const response = await fetch(`http://127.0.0.1:8080/user/${username}`);
        if (!response.ok) {
            throw new Error(`HTTP error: ${response.status}`);
        }
        return response.json();
    }

    async function setUser() {
        loading = true;
        error = null;
        try {
            user = await getData(username);
        } catch (err) {
            error = err.message;
            user = null;
        } finally {
            loading = false;
        }

        console.log(JSON.stringify(user, null, 2));
    }

    onMount(() => {
        setUser();
    });

    function cleanUrl(url) {
        if (!url) return url;
        return url.replace(/^"+|"+$/g, '');
    }

    const platformMap = {
        'github.com': { slug: 'github', label: 'GitHub' },
        'twitter.com': { slug: 'x', label: 'X' },
        'x.com': { slug: 'x', label: 'X' },
        'instagram.com': { slug: 'instagram', label: 'Instagram' },
        'linkedin.com': { slug: 'linkedin', label: 'LinkedIn' },
        'discord.com': { slug: 'discord', label: 'Discord' },
        'discord.gg': { slug: 'discord', label: 'Discord' },
        'youtube.com': { slug: 'youtube', label: 'YouTube' },
        'tiktok.com': { slug: 'tiktok', label: 'TikTok' },
        'twitch.tv': { slug: 'twitch', label: 'Twitch' },
        'itch.io': { slug: 'itchdotio', label: 'itch.io' },
    };

    function platformFor(url) {
        try {
            const hostname = new URL(cleanUrl(url)).hostname.replace(/^www\./, '');
            return platformMap[hostname] ?? { slug: 'link', label: hostname };
        } catch {
            return { slug: 'link', label: url };
        }
    }
</script>

<div class="profile-page">
    {#if loading}
        <p class="status">Loading...</p>
    {:else if error}
        <p class="status error">{error}</p>
    {:else if user}
        <div class="profile-card">
            <img
                class="profile-pic"
                src={cleanUrl(user.profile_url)}
                alt={`${user.username}'s profile picture`}
            />
            <h1 class="profile-name">{user.name ?? user.username}</h1>
            <p class="username">@{user.username}</p>

            {#if user.pronouns?.length}
                <p class="pronouns">{user.pronouns.join('/')}</p>
            {/if}

            {#if user.class_standing || user.majors?.length}
                <p class="meta-line">
                    {#if user.class_standing}{user.class_standing}{/if}
                    {#if user.class_standing && user.majors?.length} · {/if}
                    {#if user.majors?.length}{user.majors.join(', ')}{/if}
                </p>
            {/if}

            {#if user.interests?.length}
                <div class="interests">
                    {#each user.interests as interest}
                        <span class="interest-tag">{interest}</span>
                    {/each}
                </div>
            {/if}

            {#if user.bio}
                <p class="bio">{user.bio}</p>
            {/if}

            {#if user.socials?.length}
                <div class="socials">
                    {#each user.socials as social}
                        {@const platform = platformFor(social)}
                        
                            class="social-link"
                            href={cleanUrl(social)}
                            target="_blank"
                            rel="noopener noreferrer"
                        >
                            <img
                                class="social-icon"
                                src={`https://cdn.simpleicons.org/${platform.slug}`}
                                alt={platform.label}
                            />
                            <span>{platform.label}</span>
                    {/each}
                </div>
            {/if}
        </div>
    {/if}
</div>

<style>
    .profile-page {
        max-width: 600px;
        margin: 2rem auto;
        padding: 1rem;
    }
    .status {
        text-align: center;
        font-size: 1.1rem;
        color: #2b70e4;
    }
    .status.error {
        color: #c0392b;
    }
    .profile-card {
        background: white;
        border-radius: 12px;
        padding: 2rem;
        text-align: center;
    }
    .profile-pic {
        display: block;
        width: 140px;
        height: 140px;
        border-radius: 50%;
        object-fit: cover;
        border: 4px solid #ffc72c;
        margin: 0 auto 1rem;
    }
    .profile-name {
        color: #2b70e4;
        margin: 0.5rem 0 0.25rem;
    }
    .username {
        color: #888;
        margin: 0 0 0.75rem;
        font-size: 0.95rem;
    }
    .pronouns {
        color: #888;
        margin: 0 0 0.5rem;
        font-size: 0.85rem;
        font-style: italic;
    }
    .meta-line {
        color: #555;
        margin: 0 0 1rem;
        font-size: 0.9rem;
    }
    .bio {
        color: #333;
        margin: 0 0 1.5rem;
        line-height: 1.4;
    }
    .interests {
        display: flex;
        flex-wrap: wrap;
        justify-content: center;
        gap: 0.5rem;
        margin-bottom: 1.5rem;
    }
    .interest-tag {
        background: #2b70e4;
        color: white;
        padding: 0.4rem 1rem;
        border-radius: 20px;
        font-size: 0.9rem;
    }
    .socials {
        display: flex;
        flex-wrap: wrap;
        justify-content: center;
        gap: 0.75rem;
    }
    .social-link {
        display: flex;
        align-items: center;
        gap: 0.4rem;
        padding: 0.4rem 0.9rem;
        border: 2px solid #2b70e4;
        border-radius: 8px;
        color: #2b70e4;
        text-decoration: none;
        font-size: 0.9rem;
        transition: background 0.15s;
    }
    .social-link:hover {
        background: #eaf1fd;
    }
    .social-icon {
        width: 18px;
        height: 18px;
    }
</style>
