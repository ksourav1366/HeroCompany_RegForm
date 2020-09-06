Imports System.Data.SqlClient
Imports System.IO

Public Class Customer_Registration

    Dim connection As New SqlConnection("Server= SRV; Database = HERO; Integrated Security = true")



    Private Sub Button1_Click(sender As Object, e As EventArgs) Handles Button1.Click
        Dim command As New SqlCommand("insert into Hero (Owner_Name, Owner_Mobile, Owner_Address, Email_ID, Price, V_Type, Reg_No,Owner_Image,Date_Of_Purchase,Date_Of_Birth,Gender,V_Model)VALUES(@Owner_Name,@Owner_Mobile,@Owner_Address,@Email_ID,@Price,@V_Type,@Reg_No,@Owner_Image,@Date_Of_Purchase,@Date_Of_Birth,@Gender,@V_Model)", connection)

        Dim ms As New MemoryStream
        PictureBox1.Image.Save(ms, PictureBox1.Image.RawFormat)


        command.Parameters.Add("@Owner_Name", SqlDbType.VarChar).Value = TextBox1.Text
        command.Parameters.Add("Owner_Mobile", SqlDbType.VarChar).Value = TextBox2.Text
        command.Parameters.Add("@Owner_Address", SqlDbType.VarChar).Value = TextBox3.Text
        command.Parameters.Add("@Email_ID", SqlDbType.VarChar).Value = TextBox7.Text
        command.Parameters.Add("@Price", SqlDbType.VarChar).Value = TextBox4.Text
        command.Parameters.Add("@V_Type", SqlDbType.VarChar).Value = ComboBox2.Text
        command.Parameters.Add("@Reg_No", SqlDbType.VarChar).Value = TextBox6.Text
        command.Parameters.Add("@Owner_Image", SqlDbType.Image).Value = ms.ToArray()
        command.Parameters.Add("@Date_Of_Purchase", SqlDbType.Date).Value = DateTimePicker1.Value
        command.Parameters.Add("@Date_Of_Birth", SqlDbType.Date).Value = DateTimePicker2.Value
        command.Parameters.Add("@V_Model", SqlDbType.VarChar).Value = ComboBox1.Text

        Dim rdb As String = ""

        If RadioButton1.Checked = True Then
            rdb = "MALE"
        Else
            rdb = "FEMALE"
        End If

        command.Parameters.Add("@Gender", SqlDbType.VarChar).Value = rdb

        connection.Open()
        If command.ExecuteNonQuery() = 1 Then

            MessageBox.Show("Submitted Successfully")

        Else

            MessageBox.Show("Error While Submitting")

        End If

        connection.Close()

    End Sub

    Private Sub Button3_Click(sender As Object, e As EventArgs) Handles Button3.Click
        Dim opf As New OpenFileDialog
        opf.Filter = "Choose Image(*JPG;*.PNG;*.GIF)|*.jpg;*.png;*.gif"
        If opf.ShowDialog = Windows.Forms.DialogResult.OK Then
            PictureBox1.Image = Image.FromFile(opf.FileName)

        End If
    End Sub

    Private Sub Button4_Click(sender As Object, e As EventArgs) Handles Button4.Click

        View_Form.Show()


    End Sub

    Private Sub Button2_Click(sender As Object, e As EventArgs) Handles Button2.Click
        For Each control As Control In Me.Controls
            If TypeOf control Is TextBox Then
                control.Text = String.Empty
            End If
            If TypeOf control Is ComboBox Then
                control.Text = String.Empty
            End If

        Next
    End Sub
End Class