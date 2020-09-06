Imports System.Data.SqlClient
Imports System.IO

Public Class View_Form
    Dim connection As New SqlConnection("Server= SRV; Database = HERO; Integrated Security = true")
    Private Sub Button1_Click(sender As Object, e As EventArgs) Handles Button1.Click


        Dim sqlcom As New SqlCommand("Select * From Hero", connection)
        Dim da As New SqlDataAdapter(sqlcom)
        Dim dt As New DataTable
        da.Fill(dt)
        DataGridView1.DataSource = dt



    End Sub
End Class