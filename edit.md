# Edit
<form id="edit-form"><input name="title" type="text" placeholder="Title" /><textarea name="body" placeholder="Title" form="edit-form"></textarea><span id="error-msg" style="color:red;"></span><input type="submit" /></form>
<script>
    const form = document.getElementById('edit-form');
    const errMsg = document.getElementById('error-msg');
    form.addEventListener('submit', event => {
        event.preventDefault();
        const data = (new FormData(form)).forEach((value, key) => object[key] = value);
        let err = false;
        fetch('https://gh-wiki-api.programmeruser.repl.co', {
            method: 'POST',
            body: JSON.stringify(data)
        }).then(res => {
            if (!res.ok) {
                err = true;
                return res.text();
            }
        }).then(text => {
            if (err) return errMsg.textContent = text;
            else location.href = 'https://programmeruser2.github.io/wiki/wiki/' + encodeURIComponent(data.title);
        });
    });
</script>
