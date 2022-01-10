Imports System
Imports System.Windows.Controls

Namespace MyCalculatorv1
    Public Partial Class MainWindow
        Inherits Window

        Public Sub New()
            InitializeComponent()
        End Sub

        Private Sub Button_Click_1(ByVal sender As Object, ByVal e As RoutedEventArgs)
            'przycisk "B" jest przypisany calej grupie przyciskow ktorego wartosc jest rowna tekstowi zawartemu w "buttonie" , zaoszczedza to miejsca w kodzie
            Dim b As Button = CType(sender, Button)
            tb.Text += b.Content.ToString()
        End Sub
        'przycisk "wynikowy" "="
        Private Sub Result_click(ByVal sender As Object, ByVal e As RoutedEventArgs)
            Try
                result() 'wyswietlanie wyniku
            Catch __unusedException1__ As Exception
                tb.Text = "Error!" 'jesli bedzie brak danych to pojawi sie error.
            End Try
        End Sub

        Private Sub result()
            Dim op As String
            Dim iOp = 0

            If tb.Text.Contains("+") Then
                iOp = tb.Text.IndexOf("+")
            ElseIf tb.Text.Contains("-") Then
                iOp = tb.Text.IndexOf("-")
            ElseIf tb.Text.Contains("*") Then
                iOp = tb.Text.IndexOf("*")
            ElseIf tb.Text.Contains("/") Then
                iOp = tb.Text.IndexOf("/")
            Else
                'blad  
            End If

            op = tb.Text.Substring(iOp, 1)
            Dim op1 = Convert.ToDouble(tb.Text.Substring(0, iOp))
            Dim op2 = Convert.ToDouble(tb.Text.Substring(iOp + 1, tb.Text.Length - iOp - 1))

            If Equals(op, "+") Then
                tb.Text += "=" & op1 + op2
            ElseIf Equals(op, "-") Then
                tb.Text += "=" & op1 - op2
            ElseIf Equals(op, "*") Then
                tb.Text += "=" & op1 * op2
            Else
                tb.Text += "=" & op1 / op2
            End If
        End Sub
        'Przycisk "Wyjdz" odpowiadajacy za wyjscie z programu
        Private Sub Off_Click_1(ByVal sender As Object, ByVal e As RoutedEventArgs)
            Application.Current.Shutdown()
        End Sub
        'Tutaj jest przycisk "Del" , ma za zadanie usuwać całą zawartość pola z danymi
        Private Sub Del_Click(ByVal sender As Object, ByVal e As RoutedEventArgs)
            tb.Text = ""
        End Sub
        ' Przycisk R odpowiada za usunięcie ostatniej cyfry tj."BackSpace"
        Private Sub R_Click(ByVal sender As Object, ByVal e As RoutedEventArgs)
            If tb.Text.Length > 0 Then
                tb.Text = tb.Text.Substring(0, tb.Text.Length - 1)
            End If
        End Sub
        'tutaj jest pole w które będą "wstawiane" wyniki
        Private Sub tb_TextChanged(ByVal sender As Object, ByVal e As TextChangedEventArgs)
        End Sub
    End Class
End Namespace
