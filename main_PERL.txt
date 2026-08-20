use strict;
use warnings;
use diagnostics;

my @istoric;
my %operatie = (
        "add"=> "+",
        "addition"=> "+",
        "+"=> "+",
        "sub"=> "-",
        "subtraction"=> "-",
        "-"=> "-",
        "div"=> "/",
        "division"=> "/",
        "/"=> "/",
        "mul"=>"*",
        "multiplication"=> "*",
        "*"=>"*"
);

sub cleanse {
    my ($text) = @_;
    chomp($text);
    $text =~ s/^\s+|\s+$//g;
    $text = lc($text);
    return $text;
}

print "Do you want to begin? \n";
my $raspuns = <STDIN>;
$raspuns = cleanse($raspuns);

while($raspuns !~ /^(y|yes|n|no)$/){
    print "Invalid response. Type yes/y or no/n.\n";
    $raspuns = <STDIN>;
    $raspuns = cleanse($raspuns);
}

while ($raspuns =~ /^(y|yes)$/) {
    print "Great! Let's get started.\n";

    print("Operation allowed:\n");
    print("1. Addition\n");
    print("2. Subtraction\n");
    print("3. Division\n");
    print("4. Multiplication\n");
    print("Choose an operation:\n");

    $raspuns = <STDIN>;
    $raspuns = cleanse($raspuns);

    while($raspuns !~ /^(add|addition|\+|sub|subtraction|\-|div|division|\/|mul|multiplication|\*)$/){
        print("choose + - / or *\n");
        $raspuns = <STDIN>;
        $raspuns = cleanse($raspuns);
    }

    print("Select the first operand: \n");
    my $op1;
    $op1 = <STDIN>;
    $op1 = cleanse($op1);

    while ($op1 !~ /^-?\d+(\.\d+)?$/) { 
    print "The first operand must be a number. Try again.\n";
    $op1 = <STDIN>;
    $op1 = cleanse($op1);
    }

    print("Select the second operand:\n");
    my $op2;
    $op2 = <STDIN>;
    $op2 = cleanse($op2);

    while ($op2 !~ /^-?\d+(\.\d+)?$/) {
    print "The second operand must be a number. Try again.\n";
    $op2 = <STDIN>;
    $op2 = cleanse($op2);
    }

    my $rezultat;

    if($operatie{$raspuns} eq "+"){
        $rezultat = $op1 + $op2;
        push @istoric, "$op1 + $op2 = $rezultat";
        print("$op1 + $op2 = $rezultat \n");

    } elsif ($operatie{$raspuns} eq "-") {
        $rezultat = $op1 - $op2;
        push @istoric, "$op1 - $op2 = $rezultat";
        print("$op1 - $op2 = $rezultat \n");

    } elsif ($operatie{$raspuns} eq "/") {
        if ($op2 == 0) {
            print "Cannot be divided by 0.\n";
            push @istoric, "$op1 / $op2 = invalid";
        } else {
            $rezultat = $op1 / $op2;
            push @istoric, "$op1 / $op2 = $rezultat";
            print("$op1 / $op2 = $rezultat \n");
        }
        
    } elsif ($operatie{$raspuns} eq "*") {
        $rezultat = $op1 * $op2;
        push @istoric, "$op1 * $op2 = $rezultat";
        print("$op1 * $op2 = $rezultat \n");
    }

    print("Do you want to continue?\n");
    $raspuns = <STDIN>;
    $raspuns = cleanse($raspuns);

    while($raspuns !~ /^(y|yes|n|no)$/){
    print "Invalid response. Type yes/y or no/n.\n";
    $raspuns = <STDIN>;
    $raspuns = cleanse($raspuns);
    }

}

if ($raspuns =~ /^(n|no)$/){
    print "\nOkay, maybe next time.\n";
    print "\nHere is the history of your calculations:\n";
    if(@istoric==0){
        print "No calculations were made.\n";
    } else {
        for (my $i = 0; $i < @istoric; $i++) {
            print "$istoric[$i]\n";
        }
    }
    exit 0;
}