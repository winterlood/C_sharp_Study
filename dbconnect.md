DATA BASE CONNECTION WITH C#
===

>설명 추후 첨부하겠습니다.


공용 
---
**DB CONNECTION 객체 불러오는 메소드**
~~~
   private MySqlConnection getConn()
        {
            string strConn = "Server=localhost; Port=3306; Database=testdb; Uid=root;Pwd=123";
            MySqlConnection conn = new MySqlConnection(strConn);
            return conn;
        }
~~~



## REGISTER
---
>설명 추후 첨부 <BR>
> 일단 흐름 : ID 중복 체크 후, REGISTER 실행

### CODE


**ID UNIQUE CHECK METHOD**
~~~
  void  IDchk(object sender, RoutedEventArgs e)
        {
            if (inputID.Text == "")
            {
                MessageBox.Show("ID를 입력하세요");
                inputID.Focus();
                return;
            }
            MySqlConnection conn = getConn();
            conn.Open();
            string sql1 = "SELECT * FROM members WHERE id='" + inputID.Text + " '";
            MySqlCommand cmd1 = new MySqlCommand(sql1, conn);
            MySqlDataReader read = cmd1.ExecuteReader();
            if (read.Read())
            {
                conn.Close();
                ImageBrush br = new ImageBrush();
                resultIDchk.Text = "중복된 아이디 입니다!";
            }
            else
            {
                conn.Close();
                resultIDchk.Text = "사용할 수 있는 아이디 입니다!";
            }
        }
~~~

**REGISTER METHOD**

~~~
private void Register_Click(object sender, RoutedEventArgs e)
        {
           if(inputID.Text == null)
            {
                MessageBox.Show("ID를 입력하세요");
                inputID.Focus();
                return;
            }
            if (inputPW.Text == null)
            {
                MessageBox.Show("PW를 입력하세요");
                inputPW.Focus();
                return;
            }
            if (resultIDchk.Text == "사용할 수 있는 아이디 입니다!")
            {
                string sql2 = "INSERT INTO members(id, passwd) VALUES ('" + inputID.Text + "','" + inputPW.Text + "')";
                MySqlConnection conn = getConn();
                conn.Open();
                MySqlCommand cmd = new MySqlCommand(sql2, conn);
                cmd.ExecuteNonQuery();
                conn.Close();
                MessageBox.Show("회원가입 성공!");
                NavigationService.Navigate(
     new Uri("Login.xaml", UriKind.Relative));
            }
            else
            {
                MessageBox.Show("ID중복검사를 실시해 주세요.");
            }
        }
~~~


## LOGIN
---

### CODE

**로그인 메소드**
~~~
 private void Login_Click(object sender, RoutedEventArgs e)
        {
            if (inputID.Text == "")
            {
                MessageBox.Show("ID를 입력하세요");
                inputID.Focus();
                return;
            }
            if (inputPW.Text == "")
            {
                MessageBox.Show("PW를 입력하세요");
                inputPW.Focus();
                return;
            }
            string strConn = "Server=localhost; Port=3306; Database=testdb; Uid=root;Pwd=123";
            MySqlConnection conn = new MySqlConnection(strConn);
            conn.Open();
            string sql = "SELECT * FROM members WHERE id='" + inputID.Text+"'AND passwd='" + inputPW.Text + "'";
            MySqlCommand cmd1 = new MySqlCommand(sql, conn);
            MySqlDataReader read = cmd1.ExecuteReader();
            System.Console.Write("%s\n", inputID.Text);
            System.Console.Write("%s\n", inputPW.Text);
            if (read.Read())
            {      
                MessageBox.Show("로그인 성공");
                Application.Current.Properties["id"] = inputID.Text;

                Window w = new main();
                    w.Show();
                    var mainWnd = Application.Current.MainWindow as NavigationWindow;
                if(mainWnd == null)return;
                mainWnd.Close();
            }
            else MessageBox.Show("로그인 실패");
        }
~~~
