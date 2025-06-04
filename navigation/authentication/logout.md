---
layout: base
title: Logout
permalink: /logout
search_exclude: true
---

<script type="module">
    import { fetchOptions, pythonURI } from '{{site.baseurl}}/assets/js/api/config.js';
    const URL = pythonURI + '/api/authenticate';

    // Check if user is logged in (example: check for Authorization header)
    const isLoggedIn = fetchOptions.headers && fetchOptions.headers.Authorization;

    if (!isLoggedIn) {
        // Not logged in, redirect to login page
        window.location.href = "{{site.baseurl}}/login";
    } else {
        const options = {
            ...fetchOptions,
            method: 'DELETE',
        };
        console.log('Logout clicked');

        fetch(URL, options)
            .then(response => {
                if (response.ok) {
                    window.location.href = "{{site.baseurl}}/login";
                } else {
                    console.error('Logout failed:', response.statusText);
                }
            })
            .catch(error => {
                console.error('Error during logout:', error);
            });
    }
</script>
