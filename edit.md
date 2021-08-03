# Edit
<form id="edit-form"><input name="title" type="text" placeholder="Title" /><br/><textarea name="text" placeholder="Text" form="edit-form"></textarea><br/><span id="error-msg" style="color:red;"></span><br/><input type="submit" /></form>
<script>
    const form = document.getElementById('edit-form');
    const errMsg = document.getElementById('error-msg');
    form.addEventListener('submit', event => {
        event.preventDefault();
        let data = {};
        (new FormData(form)).forEach((value, key) => data[key] = value);
        let err = false;
        fetch('https://gh-wiki-api.programmeruser.repl.co/edit', {
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
        }).catch(err => errMsg.textContent = err.message);
    });
</script>
